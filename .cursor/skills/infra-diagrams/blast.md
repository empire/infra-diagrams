# Blast-radius overlays

A blast view is a **filter** over the same model. Tag the dependents, then project.

## Completion

Done when (1) every service that fails or degrades when the subject dies carries a tag, and (2) a named `view` includes those elements and colors the subject red.

## Write

1. Tags in `specification` (`#uses-redis`, `#uses-postgres`, `#critical-path`). Already in `model/spec.c4`.
2. Put tags **first** inside the element block (LikeC4 requires this).
3. Named view, explicit includes (do not rely on a clever `where` if a simple list is clearer):

   ```
   view blast_redis {
     title 'Blast: Redis down'
     include promise.panel.api
     include promise.pricing.api
     include promise.datastore.redis
     include promise.panel.api -> promise.datastore.redis
     style promise.datastore.redis { color red }
     style promise.panel.api, promise.pricing.api { color amber }
   }
   ```

4. Title states the failure: `Blast: Redis down`, not `Overview 2`.

## Scope

- Logical blast (who calls whom): this file.
- Deployment blast (which VMs share a zone): add a `deployment view` that includes that zone. Do not merge both stories into one picture unless the user asked for a combined overlay.

## Do not

- Color nodes in a landscape view and call it blast-radius. The blast view must be a separate named view.
- Mark a hop as blasted if the model has no relationship to the subject.
