<p align="center" class="logo-section">
<img src="https://i.ibb.co/31bY6kK/codicon-gist-secret.png" height="80" width="80"/>
</br>
<img src="https://halitsever-api.vercel.app/api/repo-title?title=Docker+Secret">

<p align="center">
🧰 Utility for retrieving docker secrets.<br>
<br/>
<br/>
</p>
<p align="center">
<a align="center" href="#">Documentation</a>
  </p>
</p>

<a align="center">
<img src="https://halitsever-api.vercel.app/api/details"/>
</a>

- 🐳 [**Docker**](#) - You can access secrets from docker's secrets file on nodejs

<a align="center" >
<img src="https://halitsever-api.vercel.app/api/installation"/>
</a>

Installation:

```bash
npm install @risingdijital/docker-secret --save
```

Given that you have created secrets for your docker swarm

```
printf "myUsername" | docker secret create USERNAME -
printf "mySuperSecret" | docker secret create PASSWORD -
```

You can retrieve secrets via the following methods:

### `secrets`

Loads secrets defined in the `/run/secrets` directory. To load from a different directory, refer to [`getSecrets(dir)`](#getsecretsdir).

```ts
import { secrets } from "docker-secret";

// Use secrets in your app.
mongoose.connect(
  `mongodb://${secrets.USERNAME}:${secrets.PASSWORD}@mongodb/mydb`
);
```

### `getSecrets<Secrets>(dir?: string): Secrets`

You can read secrets from a directory you define. This is useful for loading secrets from a different directory during development.

```ts
import { getSecrets } from "docker-secret";

// Without typings works fine
const secrets = getSecrets(process.env.SECRET_DIR);

secrets.USERNAME; // no error
secrets.PASSWORD; // no error
secrets.RANDOM; // no error

// But using with typings is preferred
type Credentials = {
  USERNAME: string;
  PASSWORD: string;
};

const secrets = getSecrets<Credentials>(process.env.SECRET_DIR);

secrets.USERNAME; // no error
secrets.PASSWORD; // no error
secrets.RANDOM; // error

// You can also call the function without any argument to load secrets from `/run/secrets` by default.
const secrets = getSecrets<Credentials>();
```

<a align="center" href="https://github.com/halitsever/docker-secret/issues">
<img src="https://halitsever-api.vercel.app/api/issue"/>
</a>

<a align="center">
<img src="https://halitsever-api.vercel.app/api/license"/>
</a>

<p align="center">
...
</p>
