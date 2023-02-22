# svelte-tailwind-keycloak
starter for svelte with tailwind and keycloak

## Setup
- npm i (to install all dependencies).
- run keycloak on docker.
  ```
  docker run -p 8080:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:20.0.3 start-dev
  ```
- create a new realm keycloak (example: keycloak).
- inside the realm previously created create a new client (example: svelte-app).
- inside the realm previously created create a user to test the login.
- setup the password for the user previously created.
- try to login in your svelte app.


  #### ⚠️ ONLY IN DEV ENVIRONMENT ⚠️

  In client creation remember to setup the "Root URL" (example: http://localhost:8080/*), the "Valid redirect URIs" (example: *), the "Web origins" (example: *), the "Valid post logout redirect URIs" (example: *)
