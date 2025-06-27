# TEMPLATE README

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

## Revised Template Harvesting Plan

### Phase 1: Create Template Structure
- [ ] Create `process.yaml` with proper context mappings
- [ ] Set up environment variables: `SERVICE_NAME`, `DATA_SOURCE`, `ENVIRONMENT`
- [ ] Define required specifications: product info, service domain, data dictionaries
- [ ] Create test data and expected output folders

### Phase 2: Template the Configuration Files
- [ ] Convert collection YAML files to Jinja2 templates using `service.data.creates`
- [ ] Template data dictionary files using specifications dictionaries
- [ ] Create dynamic test data generation from enumerators
- [ ] Template Docker infrastructure with environment-specific configurations

### Phase 3: Environment Configuration
- [ ] Map service domain configuration to template context
- [ ] Use environment-specific backing service configurations
- [ ] Set up validation for required data dictionaries
- [ ] Configure template processing for multiple environments

### Phase 4: Testing and Validation
- [ ] Create test specifications matching Stage0 structure
- [ ] Set up expected output files for each service type
- [ ] Test template processing with different service configurations
- [ ] Validate generated configurations work with MongoDB API

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
