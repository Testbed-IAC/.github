# Testbed-IAC

Infrastructure-as-code tooling for the [FABRIC](https://fabric-testbed.net/) national research testbed. Manage FABRIC slices, nodes, networks, and components declaratively with Terraform.

[terraform-provider-cloudlab](https://github.com/CSC478-WCU/terraform-provider-cloudlab/tree/main) will soon be migrated to this ORG. 

## Ecosystem

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'primaryColor': '#6366c8', 'primaryTextColor': '#fff', 'primaryBorderColor': '#4a4db0', 'lineColor': '#a5a8e8', 'secondaryColor': '#1e1e2e', 'tertiaryColor': '#2a2a3e'}}}%%
graph LR
    classDef iac fill:#6366c8,stroke:#4a4db0,color:#fff,rx:6
    classDef external fill:#2a2a3e,stroke:#6366c8,color:#a5a8e8,rx:6
    classDef user fill:#4a4db0,stroke:#4a4db0,color:#fff,rx:6

    U([You]):::user --> TF[HCL Config]:::iac
    TF -->| pre-built topologies| MOD[terraform-fabric-modules]:::iac
    MOD --> P[terraform-provider-fabric]:::iac
    TF -->|slice lifecycle CRUD| P
    P -->|builds & serializes FIM topology| FIM[fabric-go-fim]:::iac
    FIM -->|GraphML topology| ORC[fabric-orchestrator-go-client]:::iac
    ORC -->|REST: submit, poll, delete| CF([FABRIC Control Framework]):::external
```

## Repositories

| Repository                                                                                    | Description                                                                                                                                                                                        |
| --------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [terraform-provider-fabric](https://github.com/Testbed-IAC/terraform-provider-fabric)         | Terraform provider for FABRIC. Published on the [Terraform Registry](https://registry.terraform.io/providers/Testbed-IAC/fabric). Manages slices, nodes, components, networks, and facility ports. |
| [terraform-fabric-modules](https://github.com/Testbed-IAC/terraform-fabric-modules)           | Reusable Terraform modules built on top of the provider. Composable building blocks for common FABRIC topologies.                                                                                  |
| [fabric-go-fim](https://github.com/Testbed-IAC/fabric-go-fim)                                 | Go port of the FABRIC Information Model. Builds and serializes FIM topologies consumed by the provider.                                                                                            |
| [fabric-orchestrator-go-client](https://github.com/Testbed-IAC/fabric-orchestrator-go-client) | Go client for the FABRIC Orchestrator REST API. Handles slice lifecycle, sliver state, and POA requests.                                                                                           |

## License

All repositories in this organization are licensed under [MIT](https://opensource.org/licenses/MIT).
