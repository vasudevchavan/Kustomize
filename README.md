# Kustomize Examples

This repository demonstrates various Kustomize patterns for Kubernetes application management.

**Referance document**
https://kubectl.docs.kubernetes.io/references/kustomize/

## Base Application

The `baseapplication/` directory contains the base Kubernetes resources:
- Namespace definition
- Deployment configuration

## Examples

### 01-direct-resources: Direct Resource References
**Path:** `01-direct-resources/`

Demonstrates direct resource inclusion in kustomization.yaml:
```yaml
resources:
  - baseapplication/01-namespace.yaml
  - baseapplication/02-deployment.yaml
```

### 02-base-reference: Base Directory Reference
**Path:** `02-base-reference/`

Shows how to reference an entire base directory:
```yaml
resources:
  - ../baseapplication
```

### 03-overlays: Overlay Pattern with Environment-Specific Configurations
**Path:** `03-overlays/environments/`

Implements the overlay pattern with dev and prod environments:

**Features:**
- Environment-specific patches
- Name prefixes and suffixes
- Common labels
- Secret generation
- Strategic merge patches

**Dev Environment:**
- Prefix: `dev-`
- Suffix: `-dev`
- Custom image: `alpine:2025`
- Image pull secrets

**Prod Environment:**
- Prefix: `prod-`
- Suffix: `-prod`
- Production-specific patches


## Usage

```bash
# Build direct resources
kustomize build 01-direct-resources/

# Build base reference
kustomize build 02-base-reference/

# Build dev overlay
kustomize build 03-overlays/environments/dev/

# Build prod overlay
kustomize build 03-overlays/environments/prod/
```



## Future Addition
We are building a scenario to demonstrate how Kustomize components can serve as reusable, pluggable parts of configuration that can be optionally applied to a base configuration. This allows teams to modularize features—like logging, monitoring, or network policies—without modifying the core application definition.
