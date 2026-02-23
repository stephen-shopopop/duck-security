---
layout: center
---

# Design patterns - other

Les patterns design spécifique à nodejs:

---
layout: center
---

# Table des matières

- Optionnal pattern
- EventEmitter
- Explicit Resource Management
- Context Management
- Diagnostic channel
- Surveillance des performances
- Gestion des erreurs

---
layout: two-cols
---

# Optionnal pattern

L' "optional pattern" est un modèle de conception permettant de gérer les paramètres optionnels de manière claire et flexible lors de la définition de fonctions ou de méthodes. Il est particulièrement utile lorsqu'une fonction comporte de nombreux paramètres, la plupart ayant des valeurs par défaut raisonnables, et que vous souhaitez fournir une API plus intuitive et plus expressive aux appelants.

Ce modèle est souvent implémenté à l'aide d'options fonctionnelles et d'une classe.

::right::

```ts
import assert from 'node:assert';

type Option = (client: Client) => void;

class Client {
  age: number | undefined;
  name = 'stephen'; // default value
  type!: string; // The value is ambiguous and should be specified by the implementing class or interface.
  constructor(...options: Readonly<Option[]>) {
    for (const option of options) option(this);
    assert(this.type, new Error('type must be present'));
    // Add this to evict mutate after new instance use Object.freeze(this);
  }
}

const withName = (name: string): Option => { return (c: Client): void => { c.name = name; }; };
const withType = (type: string): Option => { return (c): void => { c.type = type; }; };
const withAge = (age: number): Option => { return (c): void => { assert(age > 0 && age % 1 === 0); c.age = age; }; };

const client1 = new Client(withAge(40), withName('John'), withType('developer'));
console.log(client1); // Client { age: 40, name: 'John', type: 'developer' }

// Use case with object - The object is sealed using `Object.seal`, preventing addition or removal of properties,
const client2: Client = Object.seal({ age: undefined, name: 'stephen', type: 'author' });
withName('Michel')(client2);
withAge(2)(client2);
console.log(client2); // { age: 2, name: 'Michel', type: 'author' }
```

---
layout: two-cols
---

# EventEmitter pattern

EventEmitters'agit d'une classe fondamentale de Node.js qui facilite l'émission et la gestion des événements. Elle permet de créer et d'écouter des événements, facilitant ainsi la gestion des opérations asynchrones et la création d'applications modulaires et maintenables.

::right::

```ts
import EventEmitter from 'node:events';

interface User {
  Id: number;
}

type Events = {
  'user-event': (event: User) => void
}

export class UsersEvent extends EventEmitter {
    override on<E extends keyof Events>(event: E, listener: Events[E]): this {
        return super.on(event, listener);
    }
    override once<E extends keyof Events>(event: E, listener: Events[E]): this {
        return super.once(event, listener);
    }
    override emit<E extends keyof Events>(event: E, ...args: Parameters<Events[E]>): boolean {
        return super.emit(event, ...args);
    }
}

const event = new UsersEvent();

const handleUserEvent = (user: User) => console.log(user);
event.on('user-event', event => handleUserEvent.catch(error => console.error(error)));
event.emit('user-event', { id: 42 });
```

---
layout: two-cols
---

# Explicit Resource Management

La gestion explicite des ressources introduit une approche déterministe pour gérer explicitement le cycle de vie des ressources telles que les descripteurs de fichiers, les connexions réseau, etc - [ref](https://v8.dev/features/explicit-resource-management)

```ts
class Message implements Disposable {
  value = 'hello';
  [Symbol.dispose]() {
    console.log('Resource disposed');
    this.value = ''world;
  }
}

let msg: Message;
{
  using message = new Message();
  msg = message
  console.log(message.value); // hello
}
console.log(msg.value); // world
```

::right::

```ts
export class Dependency<Service> implements Disposable {
  #serviceInjected: Service | undefined;
  #serviceCached: Service | undefined;
  #stack = new DisposableStack();
  constructor(
    private serviceInitializer: () => Service | Promise<Service>,
    private cacheable = true
  ) {
    this.#stack.adopt(this.injection, () => { this.#serviceInjected = undefined; });
  }
  injection(service: Service): this {
    this.#serviceInjected = service;
    return this;
  }
  clearInjected(): this {
    this.#serviceInjected = undefined;
    return this;
  }
  async resolve(): Promise<Service> {
    if (this.#serviceInjected) { return this.#serviceInjected; }
    if (!this.cacheable) { this.#serviceCached = undefined; }
    return (this.#serviceCached ??= await this.serviceInitializer());
  }
  async [Symbol.dispose]() { this.#stack.dispose(); }
}
```

---
layout: two-cols
---

# Context Management

Le context management est utilisé pour associer l'état et le propager à travers les rappels et les chaînes de promesses. Ils permettent de stocker des données tout au long de la durée de vie d'une requête Web ou de toute autre durée asynchrone. Il est similaire au stockage local de threads dans d'autres langues.

::right::

```ts
import http from 'node:http';
import { parseArgs } from 'node:util';
import { AsyncLocalStorage } from 'node:async_hooks';

const asyncLocalStorage = new AsyncLocalStorage();

const server = http.createServer((_req, res) => {
  asyncLocalStorage.run(new Map(), () => {
    const store = asyncLocalStorage.getStore();
    store.set('requestId', Math.random().toString(36).substring(2, 15));

    res.setHeader('content-type', 'application/json; charset=utf-8');
    res.end(JSON.stringify({ hello: 'world', requestId: store.get('requestId') }));
  });
});

server.listen(3000);
```

---
layout: two-cols
---

# Diagnostic channel

Node.js comprend des capacités de diagnostic sophistiquées qui vous aident à comprendre ce qui se passe dans votre application.

::right::

```ts
import diagnostics_channel from 'node:diagnostics_channel';

const dbChannel = diagnostics_channel.channel('app:database');
dbChannel.subscribe((message) => { console.log('Database operation:', message); });

async function queryDatabase(sql, params) {
  const start = performance.now();
  try {
    const result = await db.query(sql, params);
    dbChannel.publish({
      operation: 'query',
      sql,
      params,
      duration: performance.now() - start,
      success: true
    });
    return result;
  } catch (error) {
    dbChannel.publish({
      operation: 'query',
      sql,
      params,
      duration: performance.now() - start,
      success: false,
      error: error.message
    });
    throw error;
  }
}
```

---
layout: two-cols
---

# Surveillance des performances

La surveillance des performances est désormais intégrée à la plate-forme, éliminant ainsi le besoin d'outils APM externes pour la surveillance de base.

::right::

```ts
import Fastify from 'fastify';
import { PerformanceObserver, performance } from 'node:perf_hooks';

const obs = new PerformanceObserver((list) => {
  const entries = list.getEntries();
  entries.forEach((entry) => {
    console.log(`${entry.entryType} - ${entry.name}: ${entry.duration} milliseconds`);
  });
});

obs.observe({ entryTypes: ['measure', 'function', 'http', 'dns'] });

const task = () => {
  performance.mark('startTask');
  for (let i = 0; i < 500000000; i++) {}
  performance.mark('endTask');
  performance.measure('Task Execution Time', 'startTask', 'endTask');
};

const fastify = Fastify();

fastify.get('/', (_request, reply) => {
  task();
  reply.send({ hello: 'world' });
});

fastify.listen({ port: 3000 });
```

---
layout: two-cols
---

# Gestion des erreurs

Les applications modernes bénéficient d'une gestion des erreurs structurée et contextuelle qui fournit de meilleures informations de débogage

::right::

```ts
class AppError extends Error {
  constructor(message, code, statusCode = 500, context = {}) {
    super(message);
    this.name = 'AppError';
    this.code = code;
    this.statusCode = statusCode;
    this.context = context;
    this.timestamp = new Date().toISOString();
  }
  toJSON() {
    return {
      name: this.name,
      message: this.message,
      code: this.code,
      statusCode: this.statusCode,
      context: this.context,
      timestamp: this.timestamp,
      stack: this.stack
    };
  }
}

throw new AppError(
  'Database connection failed',
  'DB_CONNECTION_ERROR',
  503,
  { host: 'localhost', port: 5432, retryAttempt: 3 }
);
```
