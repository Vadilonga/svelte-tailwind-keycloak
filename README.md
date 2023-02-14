# svelte-tailwind-keycloak
starter for svelte with tailwind and keycloak

## Setup
- run keycloak on docker
  ```
  docker run -p 8080:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:20.0.3 start-dev
  ```

- create a new realm keycloak (example: keycloak), a new client (example: svelte-app) and a user to test the login.

- try to login in your svelte app

  #### ⚠️ ONLY IN DEV ENVIRONMENT ⚠️

  In client creation remember to setup the "Root URL" (example: http://localhost:8080/*), the "Valid redirect URIs" (example: *), the "Web origins" (example: *).
