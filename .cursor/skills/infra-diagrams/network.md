# On-prem network / VM / VLAN

Deployment is a second layer. It points at the logical model. It does not replace it.

## Completion

Done when a `deployment view` shows the asked zones (or VLANs) and every running process is `instanceOf` a logical element, not a free-floating box.

## Write

1. Node kinds in `specification`: `environment`, `zone`, `vlan`, `vm`. Optional extras (`rack`, `hypervisor`) only if the user named them.
2. Nest: environment → zone (or VLAN) → vm. Put the CIDR in the zone `description` or the VM `technology` field (IP).
3. Place workloads with `instanceOf <logical.element>` inside the VM. One VM may instance more than one component.
4. Views:

   ```
   deployment view onprem { include env.** }
   deployment view data_plane { include env.z_data.** }
   ```

## Promise sample

`model/deploy.c4` uses fictional `10.50.x.0/24` zones: edge, apps, data, msg, k8s. Replace CIDRs and hostnames when the user provides inventory. Do not copy a live map into the sample by default.

## Do not

- Invent peering or firewall rules the user did not state. Draw the zones they named.
- Put Kubernetes objects in a bare `vm` unless they actually run as a single VM. Use [k8s.md](k8s.md).
