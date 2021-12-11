# Practical Byzantine Fault-Tolerance in Ivy

## Check Abstract Model

1. Axioms cannot be compiled with the implementation and hence are commented out by default. Uncomment the axioms in `pbft_abstract_kv.ivy`.
2. Uncomment the exported actions situated at the end of the file.

To verify
```bash
ivy_check pbft_abstract_kv.ivy
```

A successful run should report `OK` in the end.

## Build and Run

```bash
ivyc target=test kv.ivy
ivy_launch node.max=3 client_t.max=1 key_t.max=1 iters=1000 kv.ivy
```

The arguments can be modified accordingly.

## Code Organisation and Config

| File                    | Description                                            |
| ------------------------| ------------------------------------------------------ |
| [`kv.ivy`](kv.ivy)      | Client Implementation and KV-store instantiation       |
| [`servers.ivy`](servers.ivy)               | PBFT Server Implementation           |
| [`pbft_spec.ivy`](pbft_spec.ivy) | PBFT Specification and KV-store interface |
| [`pbft_abstract_kv.ivy`](pbft_abstract_kv.ivy) | Abstract Model                   |
| [`cs_network.ivy`](cs_network.ivy) | Client-Server network overlay and message definitions |
| [`indexset.ivy`](indexset.ivy) | Modified indexset with support for the `supermajority` relation |
| [`server_message_types.ivy`](server_message_types.ivy) | Message definitions for inter-server network overlay |
| [`sign.ivy`](sign.ivy) | Signature specification model |

To disable nodes acting maliciously, uncomment the following line in `kv.ivy`

```
attribute fault.weight = "0"
```

Weights of all other actions can be configured as needed.