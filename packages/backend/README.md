# example-backend

This package is an EXAMPLE of a Backstage backend.

The main purpose of this package is to provide a test bed for Backstage plugins
that have a backend part. Feel free to experiment locally or within your fork by
adding dependencies and routes to this backend, to try things out.

Our goal is to eventually amend the create-app flow of the CLI, such that a
production ready version of a backend skeleton is made alongside the frontend
app. Until then, feel free to experiment here!

## Development

To run the example backend, first go to the project root and run

```bash
yarn install
```

You should only need to do this once.

After that, go to the `packages/backend` directory and run

```bash
yarn start
```

If you want to override any configuration locally, for example adding any secrets,
you can do so in `app-config.local.yaml`.

The backend starts up on port 7007 per default.

## Populating The Catalog

If you want to use the catalog functionality, you need to add so called
locations to the backend. These are places where the backend can find some
entity descriptor data to consume and serve. For more information, see
[Software Catalog Overview - Adding Components to the Catalog](https://backstage.io/docs/features/software-catalog/#adding-components-to-the-catalog).

To get started quickly, this template already includes some statically configured example locations
in `app-config.yaml` under `catalog.locations`. You can remove and replace these locations as you
like, and also override them for local development in `app-config.local.yaml`.

## Authentication

We chose [Passport](http://www.passportjs.org/) as authentication platform due
to its comprehensive set of supported authentication
[strategies](http://www.passportjs.org/packages/).

Read more about the
[auth-backend](https://github.com/backstage/backstage/blob/master/plugins/auth-backend/README.md)
and
[how to add a new provider](https://github.com/backstage/backstage/blob/master/docs/auth/add-auth-provider.md)

## Documentation

- [Backstage Readme](https://github.com/backstage/backstage/blob/master/README.md)
- [Backstage Documentation](https://backstage.io/docs)

# Backstage and PostgreSQL Docker Setup

This repository contains the setup for running Backstage with a PostgreSQL database using Docker Compose. Both services are built to run on the same custom Docker network.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [Node.js](https://nodejs.org/en/) and [Yarn](https://classic.yarnpkg.com/en/docs/install)

## Project Structure

├── docker-compose.yml
├── README.md
├── packages
│ └── backend
│   ├── Dockerfile
│ └── (other backend source files)
└── (other files)

## Build Instructions

Before building and running the Docker containers, you need to build your Backstage project locally:

1. **Install Dependencies:**

   ```bash
   yarn install --frozen-lockfile

2. **Compile TypeScript:**

    ```bash
    yarn tsc
    
3. **Build the Backend:**
    ```bash
    yarn build:backend

4. **Build the Docker Image: If you prefer building the Docker image manually, run:**
    ```bash
    docker image build . -f packages/backend/Dockerfile --tag backstage:1.0.0

Alternatively, Docker Compose will build the image for you when using the build instruction in the Compose file.

## Running the Application

1. **Start the Services with Docker Compose:**

    ```bash
    docker-compose up --build

This command will:

- **Build the Backstage image** (if not already built).
- **Start both the PostgreSQL and Backstage containers** on the `backstage-net` network.
- **Map PostgreSQL on host port 5432** and **Backstage on host port 7007**.

### Accessing the Services

- **Backstage:**  
  Open a browser and navigate to [http://localhost:7007](http://localhost:7007).

- **PostgreSQL:**  
  You can use pgAdmin or any PostgreSQL client to connect to `localhost:5432` using the following credentials:
  - **User:** backstage  
  - **Password:** 1234  
  - **Database:** backstage_db

