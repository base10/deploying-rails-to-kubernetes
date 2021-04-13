# Lab 2 - Creating Docker and Kubernetes configurations

## Overview

In this lab we will look through the Dockerfile and Kubernetes configuration
files, as well as the health check that will be used on the pods.

## Procedure

### Step 1 - Examine Dockerfile

A few lines of note:

1. We set the application's port: `ENV PORT 3000`

2. We build the backend of the application: `RUN bundle install`

3. We build the frontend of the application:

`RUN yarn upgrade webpack@^4.0.0 && bundle exec rake assets:precompile`

4. We start the Puma server at the end:

`CMD ["bundle", "exec", "puma", "-C", "config/puma.rb"]`

### Step 2 - Examine app deployment yaml

1. We select the type of resource: `kind: "Deployment"`
2. We specify the name of the app: `name: "link-app"`
3. We specify the container image: `image: link-container`
4. Because the image will be local, we add `imagePullPolicy: Never`
5. We configure the requested resources in the `resources` section.
6. We provide values for environment variables:
```
        env:
        - name: "DATABASE_URL"
          value: "postgresql://postgres@172.16.100.20:5432/link"
        - name: "REDIS_URL"
          value: "redis://172.16.100.20:6379/15"
```

### Step 3 - Examine app service yaml

1. We select type of resource: `kind: "Service"`
2. We specify the name of the app: `name: "link-app"`
3. We specify the port mapping for incoming requests:
```
    port: 3000
    targetPort: 3000
    nodePort: 30000
```

### Step 4 - Examine sidekiq deployment yaml

This file is very similar to the app deployment yaml. It includes this section
to indicate what app deploymenty it is connected to:
```
  selector:
    matchLabels:
      app: "link-app"
```

### Step 5 - Examine health check

You can find the health check under `lib/health_check.rb`. It has been
implemented as rack middleware for the purposes of this workshop. You can find
the health check configured under each different environment in
`config/environments`.
