# Terraform
- [Commands](#commands)
- [Detect changes](#detect_changes)

## Commands <a name="commands"></a>
Most common terraform commands:
- terraform plan - Creates a roadmap of the changes Terraform will make to your infrastructure – showing what will be created, modified, or deleted.
- terraform apply - Implements infrastructure changes according to plan

## Detect changes <a name="detect_changes"></a>
- Terraform reads the state file
- Queries the real infrastructure in the cloud
- Compares state file and state from cloud
- Creates a plan of changes