# Kubernetes topology

Same deployment layer as VMs. The cluster is a `deploymentNode`.

## Completion

Done when a `deployment view` shows cluster → namespace → workload, and the workload is `instanceOf` the logical service. Ingress/Service extra boxes go in Mermaid only if the user asked for those Kubernetes kinds by name.

## Write

1. Kinds (already in `model/spec.c4`): `kubernetes`, `namespace`, `workload`.
2. Nest under the on-prem zone that owns the cluster:

   ```
   zone 'zone-k8s' {
     kubernetes 'promise-k8s' {
       namespace 'pricing' {
         workload 'pricing-deploy' {
           instanceOf promise.pricing.api
         }
       }
     }
   }
   ```

3. View: `deployment view k8s { include env.z_k8s.** }`.
4. If the user wants Ingress / Service / Endpoints spelled out, add `mermaid/k8s-*.mmd` as a flowchart. LikeC4 has no first-class Ingress kind; do not fake one as a `service` in the logical model unless it is a real Promise service.

## Do not

- Draw every Pod replica unless the user asked for replica count.
- Mix cloud-vendor C4 icons (`aws:`, `gcp:`) into an on-prem cluster. Use `tech:kubernetes`.
