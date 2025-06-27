I think# TEMPLATE README

This is a stage0 template repo for creating MongoDB Configuration APIs.

## Analysis of Working Project

The `stage0_template_mongodb_api` project is a working MongoDB Configuration API that provides:
- **Collection Management**: YAML-based collection definitions with versioning and indexing
- **Data Dictionary**: Simple Schema definitions for data types and validation
- **Test Data**: JSON files with sample data for each collection
- **Docker Infrastructure**: Complete containerized setup with MongoDB, API, and SPA
- **Development Tools**: Makefile for testing and production workflows

### Key Components to Harvest:

1. **Collection Configuration Files** (`input/collections/*.yaml`)
   - Define MongoDB collections with versioning
   - Specify indexes and constraints
   - Reference test data files

2. **Data Dictionary** (`input/dictionary/*.yaml`)
   - Simple Schema type definitions
   - Property validation rules
   - Custom type definitions in `types/` subdirectory

3. **Test Data** (`input/data/*.json`)
   - Sample data for each collection
   - Enumerators for dropdown values
   - Realistic test scenarios

4. **Infrastructure Templates**
   - `docker-compose.yaml` for container orchestration
   - `Dockerfile` for API container
   - `makefile` for development workflows

5. **Documentation**
   - API documentation in `docs/`
   - OpenAPI specifications
   - Usage examples

## Specifications Analysis

After reviewing the Stage0 specifications, I understand the data structure that will drive this template:

### Architecture Context
- **Product**: `stage0` - Stage Zero platform
- **Organization**: `agile-learning-institute` - The Agile Learning Institute
- **Domain**: `mongodb` - MongoDB database configuration utility
- **Environment**: Multiple environments (DEV, TEST, STAGE, PROD) with MongoDB backing services

### Data Dictionary Structure
The specifications contain dictionaries for:
- **Core Entities**: `user`, `organization`, `product`, `workshop`, `chain`, `exercise`
- **Bot System**: `bots`, `conversation`, `runbook`, `template`
- **Observations**: Various observation types for design thinking
- **Enumerators**: Status values and system constants

### Template Context Mapping
The template will use:
- **Service Context**: From `architecture.domains` filtered by `SERVICE_NAME`
- **Data Sources**: From `service.data.creates` and `service.data.consumes`
- **Product Info**: From `product.yaml` (name, description, organization)
- **Data Dictionaries**: From `dictionaries/` folder matching the service's data sources

## Detailed Template Harvesting Plan

### Phase 1: File Consolidation and Generic Templates
- [ ] **Identify duplicate files** that will be generated from single templates
- [ ] **Delete duplicates** and create generic template files with descriptive names
- [ ] **Collection templates**: Create `collection.yaml.template` for all collection configs
- [ ] **Data templates**: Create `data.json.template` for all test data files
- [ ] **Dictionary templates**: Create `dictionary.yaml.template` for all dictionary files

### Phase 2: Template Variable Identification and Replacement
- [ ] **Basic transformations**:
  - Replace `agile-learning-institute` with `{{organization}}`
  - Replace `stage0` with `{{product}}`
- [ ] **Collection configuration templates**:
  - Iterate over `data_catalog.dictionaries` to generate collection configs
  - Template collection names, descriptions, and test data references
- [ ] **Dictionary file processing**:
  - Copy all dictionaries from specifications as-is
  - Add `.1.0.0` version suffix to filenames
  - Template organization and product references
- [ ] **Types directory**: Copy all types as-is (no templating needed)

### Phase 3: Infrastructure and Documentation Templating
- [ ] **Docker files**: Template organization and product references
- [ ] **Makefile**: Template service names and ports
- [ ] **README.md**: 
  - Add template-specific text that gets removed during processing
  - Template organization and product references
  - Add references to template README that get cleaned up
- [ ] **Documentation**: Template API docs and OpenAPI specs

### Phase 4: Process Configuration and Testing
- [ ] **Create `process.yaml`** with proper context mappings
- [ ] **Environment variables**: `SERVICE_NAME`, `DATA_SOURCE`, `ENVIRONMENT`
- [ ] **Template processing rules**:
  - Single file merges for infrastructure files
  - `mergeFor` loops for collections based on `data_catalog.dictionaries`
  - `mergeFor` loops for test data files
- [ ] **Test data setup**: Create specifications structure for testing
- [ ] **Expected output**: Generate expected files for validation

## File Transformation Details

### Collection Configuration Files
**Template**: `input/collections/collection.yaml.template`
**Generation**: One file per dictionary in `data_catalog.dictionaries`
**Variables**:
- `{{collection_name}}` - Dictionary name
- `{{collection_title}}` - Dictionary title
- `{{collection_description}}` - Dictionary description
- `{{test_data_file}}` - Generated test data filename

### Data Dictionary Files
**Source**: `specifications/dictionaries/*.yaml`
**Destination**: `input/dictionary/{{dictionary_name}}.1.0.0.yaml`
**Transformations**:
- Replace organization references
- Replace product references
- Keep all schema definitions intact

### Test Data Files
**Template**: `input/data/data.json.template`
**Generation**: One file per dictionary in `data_catalog.dictionaries`
**Variables**:
- `{{collection_name}}` - Dictionary name
- `{{sample_data}}` - Generated sample data based on schema

### Infrastructure Files
**Files to template**:
- `docker-compose.yaml` - Organization and product references
- `Dockerfile` - Organization references
- `makefile` - Service-specific configurations
- `README.md` - Organization, product, and template references

## Template Usage

Once harvested, this template will generate:
- Complete MongoDB Configuration API setup for any Stage0 service
- Customizable collection definitions based on service data sources
- Data validation schemas from Stage0 specifications
- Environment-specific containerized development environments
- API documentation and testing tools

## Environment Variables

The template will require these environment variables:
- `SERVICE_NAME`: The service domain name (e.g., "mongodb", "search", "cat_bot")
- `DATA_SOURCE`: Primary data dictionary to focus on
- `ENVIRONMENT`: Target environment (DEV, TEST, STAGE, PROD)

## Current Test Command

```bash
TEMPLATE_TEST.sh

rm -rf ~/tmp/testRepo
cp -r ./* ~/tmp/testRepo

docker run --rm \
    -v ~/tmp/testRepo:/repo 
    -v ./test_data:/specifications 
    -e SERVICE_NAME=mongodb \
    -e DATA_SOURCE=user \
    -e ENVIRONMENT=DEV \
    ghcr.io/agile-learning-institute/stage0_runbook_merge:latest
```
