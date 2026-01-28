# CSAPI Validation Capabilities Reference

**Last Updated:** January 28, 2026  
**Repository:** [OS4CSAPI/ogc-client-CSAPI](https://github.com/OS4CSAPI/ogc-client-CSAPI)  
**Validated Commit:** `a71706b9592cad7a5ad06e6cf8ddc41fa5387732`

---

## Overview

This document provides a comprehensive, accurate reference for validation capabilities in the OGC-Client-CSAPI library. It clearly distinguishes between what validations **ARE implemented** and what validations **are NOT implemented** (despite claims that may exist in other documentation).

**Purpose:** Prevent confusion, runtime errors, and incorrect assumptions about validation scope by documenting actual capabilities.

**Critical Note:** All validators use **structural validation** (manual type checking, property validation) rather than **schema-based validation** (fetching and validating against OGC JSON schemas). This is an important architectural distinction.

---

## Validation Approach

### ✅ What IS Used: Structural Validation

All three validation systems (GeoJSON, SWE Common, SensorML) implement **manual structural validation**:

- **Type Checking:** Runtime TypeScript type guards and discriminators
- **Required Properties:** Explicit checks for mandatory fields (uid, featureType, definition, etc.)
- **Type-Specific Rules:** Custom validation logic for each resource/component type
- **Constraint Validation:** Interval checking, pattern matching, format validation
- **Manual Property Inspection:** Direct object property access and validation

**Advantages:**
- Fast execution (no network requests)
- No external dependencies
- Predictable behavior
- Works offline

**Limitations:**
- Not guaranteed to match OGC JSON schemas exactly
- Must be manually updated when specifications change
- May miss subtle schema violations

### ❌ What is NOT Used: Schema-Based Validation

Despite documentation claims, the validators do **NOT**:

- ❌ Fetch OGC JSON schemas from `schemas.opengis.net`
- ❌ Validate using Ajv (Another JSON Schema Validator) against fetched schemas
- ❌ Cache downloaded schemas for performance
- ❌ Provide JSON Schema compliance guarantees

**Why This Matters:** Users expecting strict OGC JSON Schema compliance should be aware that validation is structural and may not catch all schema violations.

---

## GeoJSON Validation System

**Location:** `src/ogc-api/csapi/validation/geojson-validator.ts`  
**Test Count:** 61 tests  
**Code Coverage:** 40.95%

### ✅ Implemented Validators

**Feature Validators (7 types):**
- `validateSystemFeature(feature)` - System/Sensor feature validation
- `validateDeploymentFeature(feature)` - Deployment feature validation
- `validateProcedureFeature(feature)` - Procedure feature validation
- `validateSamplingFeature(feature)` - Sampling Feature validation
- `validatePropertyFeature(feature)` - Observable/Controllable Property validation
- `validateDatastreamFeature(feature)` - Datastream feature validation
- `validateControlStreamFeature(feature)` - Control Stream feature validation

**Collection Validators (7 types):**
- `validateSystemFeatureCollection(collection)` - Validates FeatureCollection of Systems
- `validateDeploymentFeatureCollection(collection)` - Validates FeatureCollection of Deployments
- `validateProcedureFeatureCollection(collection)` - Validates FeatureCollection of Procedures
- `validateSamplingFeatureCollection(collection)` - Validates FeatureCollection of Sampling Features
- `validatePropertyFeatureCollection(collection)` - Validates FeatureCollection of Properties
- `validateDatastreamFeatureCollection(collection)` - Validates FeatureCollection of Datastreams
- `validateControlStreamFeatureCollection(collection)` - Validates FeatureCollection of Control Streams

**Type Guards (7 types):**
- `isSystemFeature(feature)` - Type guard for System features
- `isDeploymentFeature(feature)` - Type guard for Deployment features
- `isProcedureFeature(feature)` - Type guard for Procedure features
- `isSamplingFeature(feature)` - Type guard for Sampling Features
- `isPropertyFeature(feature)` - Type guard for Property features
- `isDatastreamFeature(feature)` - Type guard for Datastream features
- `isControlStreamFeature(feature)` - Type guard for Control Stream features

**What Each Validator Checks:**

✅ **GeoJSON Structure:**
- `type: 'Feature'` or `type: 'FeatureCollection'` present
- `properties` object exists
- `geometry` field present (nullable)

✅ **CSAPI Required Properties:**
- `uid` (unique identifier) present and non-empty
- `featureType` matches expected type (e.g., "http://www.w3.org/ns/sosa/System")
- `name` present (optional in some types)

✅ **Type-Specific Requirements:**
- **Deployments:** `system` reference link present
- **Datastreams:** `system` and `observedProperty` reference links present
- **Control Streams:** `system` and `controlledProperty` reference links present
- **Properties:** `definition` field present

✅ **Error Reporting:**
- Detailed error messages with property paths
- Error aggregation for collections (with index tracking)
- Validation result structure: `{ valid: boolean, errors: ValidationError[] }`

### ❌ NOT Implemented (Despite Documentation Claims)

**Geometry Validation:**
- ❌ Coordinate validation (no bbox checks, dimension validation)
- ❌ Geometry type checking (no validation that geometry matches expected type)
- ❌ GeometryCollection validation (basic types only: Point, LineString, Polygon, Multi*)
- ❌ Spatial relationship validation
- ❌ CRS (Coordinate Reference System) validation

**Link Validation:**
- ❌ No `validateLinks()` function exists
- ❌ No validation of `links` array structure
- ❌ No `rel` (relation) checking
- ❌ No `href` (URL) format validation
- ❌ No validation that required links are present

**Temporal Validation:**
- ❌ No `validateTemporal()` function exists
- ❌ No ISO 8601 date/time format validation
- ❌ No temporal extent validation
- ❌ No deployment period validation (despite being mentioned in validator description)
- ❌ No validation of `phenomenonTime` or `resultTime` formats

**Type-Specific Advanced Validation:**
- ❌ Deployment period structure validation
- ❌ Procedure definition/metadata validation (only checks existence)
- ❌ Sampling Feature `featureOfInterest` properties validation
- ❌ Sampling Feature spatial extent validation
- ❌ Datastream/Control Stream schema validation (only checks reference existence)

### ⚠️ Important Limitations

**Collection Validators (0% Test Coverage):**
All seven collection validators have **zero test execution coverage**. They consist primarily of iteration logic that applies single-feature validators to arrays. While the underlying validation logic IS tested, the collection-specific error aggregation and iteration code is not.

**Recommendation:** Test collection validators or use single-feature validators in loops for mission-critical validation.

### 📝 Usage Examples

**Valid Usage:**
```typescript
import { validateSystemFeature, isSystemFeature } from 'ogc-client/csapi/validation';

// Basic feature validation
const result = validateSystemFeature(feature);
if (!result.valid) {
  console.error('Validation errors:', result.errors);
}

// Type guard usage
if (isSystemFeature(feature)) {
  // TypeScript knows this is a SystemFeature
  console.log(feature.properties.name);
}
```

**What WON'T Work:**
```typescript
// ❌ These functions do NOT exist
validateGeometry(feature.geometry);  // Error: function not found
validateLinks(feature.links);        // Error: function not found
validateTemporal(feature.properties.phenomenonTime);  // Error: function not found
```

**Workarounds for Missing Validation:**

```typescript
// Manual geometry validation
function validateGeometryManually(geometry: GeoJSONGeometry): boolean {
  if (!geometry || !geometry.type) return false;
  
  switch (geometry.type) {
    case 'Point':
      return Array.isArray(geometry.coordinates) && geometry.coordinates.length >= 2;
    case 'LineString':
      return Array.isArray(geometry.coordinates) && geometry.coordinates.length >= 2;
    // ... add other types as needed
    default:
      return false;
  }
}

// Manual link validation
function validateLinksManually(links: any[]): boolean {
  if (!Array.isArray(links)) return false;
  
  return links.every(link => 
    typeof link.rel === 'string' && 
    typeof link.href === 'string' &&
    (link.href.startsWith('http://') || link.href.startsWith('https://'))
  );
}

// Manual temporal validation
function validateISO8601(dateString: string): boolean {
  const iso8601Regex = /^\d{4}-\d{2}-\d{2}T\d{2}:\d{2}:\d{2}(\.\d+)?(Z|[+-]\d{2}:\d{2})?$/;
  return iso8601Regex.test(dateString);
}
```

---

## SWE Common Validation System

**Location:** `src/ogc-api/csapi/validation/swe-validator.ts` (component validation)  
**Location:** `src/ogc-api/csapi/validation/constraint-validator.ts` (constraint validation)  
**Test Count:** 78 tests (50 component + 28 constraint)  
**Code Coverage:** 73.68%

### ✅ Implemented Validators (9 Component Validators)

**Simple Component Validators (6 types):**
- `validateBoolean(component)` - Boolean component validation
- `validateCount(component)` - Count (integer) component validation
- `validateQuantity(component)` - Quantity (decimal) component validation
- `validateText(component)` - Text component validation
- `validateCategory(component)` - Category (coded value) component validation
- `validateTime(component)` - Time component validation

**Range Component Validator (1 generic for 4 types):**
- `validateRangeComponent(component)` - Generic validator for QuantityRange, CountRange, TimeRange, CategoryRange

**Aggregate Component Validators (3 types):**
- `validateDataRecord(component)` - DataRecord (field collection) validation
- `validateDataArray(component)` - DataArray (element array) validation
- `validateObservationResult(result)` - Observation result structure validation (⚠️ UNTESTED - 0% coverage)

**Constraint Validators (3 types):**
- `validateAllowedValues(constraint, value)` - Numeric interval validation with significant figures
- `validateAllowedTokens(constraint, value)` - Text pattern/regex validation
- `validateAllowedTimes(constraint, value)` - Temporal interval validation

**Exported from `swe/index.ts`:**
```typescript
export {
  validateDataRecord,
  validateBoolean,
  validateCount,
  validateQuantity,
  validateText,
  validateCategory,
  validateTime,
  validateDataArray,
  validateObservationResult,
  validateRangeComponent,
  validateAllowedValues,
  validateAllowedTokens,
  validateAllowedTimes,
  validateSWEComponent  // Generic dispatcher
} from './swe-validator';
```

**What Each Validator Checks:**

✅ **Type Validation:**
- Correct `type` field (e.g., "Quantity", "DataRecord")
- Required type-specific properties

✅ **UoM (Unit of Measure) Validation:**
- Present where required (Quantity, QuantityRange)
- Valid structure (code, href, or symbol)

✅ **Constraint Validation:**
- `AllowedValues`: Interval checking (min/max), significant figures enforcement
- `AllowedTokens`: Pattern matching with regex support
- `AllowedTimes`: Temporal constraint validation

✅ **Aggregate Structure Validation:**
- **DataRecord:** `fields` array exists
- **DataArray:** `elementType` and `elementCount` present
- **ObservationResult:** Basic structure validation (⚠️ untested)

✅ **Reference Frame Validation:**
- Vector reference frame validation
- Coordinate system checking

### ❌ NOT Implemented (Claimed but Missing)

**Missing Component Validators (8 types):**

These validators were **claimed** in some documentation but are **NOT exported** from `swe/index.ts` and/or **NOT implemented** in `swe-validator.ts`:

1. ❌ `validateQuantityRange()` - Use `validateRangeComponent()` instead
2. ❌ `validateCategoryRange()` - Use `validateRangeComponent()` instead
3. ❌ `validateCountRange()` - Use `validateRangeComponent()` instead
4. ❌ `validateTimeRange()` - Use `validateRangeComponent()` instead
5. ❌ `validateAbstractDataComponent()` - NOT implemented
6. ❌ `validateAbstractSimpleComponent()` - NOT implemented
7. ❌ `validateGeometryData()` - NOT implemented
8. ❌ `validateNilValues()` - NOT implemented

**Missing Component Type Support:**

The generic `validateSWEComponent()` dispatcher returns `{ valid: true }` without validation for:
- ❌ `Vector` (claimed but not validated)
- ❌ `Matrix` (claimed but not validated)
- ❌ `DataStream` (claimed but not validated)
- ❌ `DataChoice` (claimed but not validated)
- ❌ `Geometry` (claimed but not validated)
- ❌ Boolean type validators for geometry types (Point, LineString, Polygon, etc.)

**Missing Specification Compliance:**
- ❌ Required OGC properties NOT validated:
  - `definition` (mandatory per OGC 24-014) - NOT checked
  - `label` (mandatory per OGC 24-014) - NOT checked
- ❌ Deep nested validation requires **manual recursive calls** (not automatic)

### ⚠️ Important Limitations

**validateObservationResult() is UNTESTED:**
This function has **0% test execution coverage** (0 calls in test suite). Use with caution or implement additional testing.

**Constraint Validation is Excellent:**
The constraint validation system (intervals, patterns, significant figures) is **comprehensively tested** and can be relied upon. This is the strength of the validation system.

**Aggregate Validation is Basic:**
`validateDataRecord()` and `validateDataArray()` check only basic structure (field array exists, element type present) without recursively validating nested component structures.

### 📝 Usage Examples

**Valid Usage:**
```typescript
import { 
  validateQuantity, 
  validateDataRecord,
  validateAllowedValues,
  validateRangeComponent  // Use this for all Range types
} from 'ogc-client/csapi/validation';

// Simple component validation
const quantityResult = validateQuantity(component);
if (!quantityResult.valid) {
  console.error('Invalid Quantity:', quantityResult.errors);
}

// Constraint validation
const constraintResult = validateAllowedValues(constraint, value);
if (!constraintResult.valid) {
  console.error('Value violates constraint:', constraintResult.errors);
}

// Range validation (generic for all range types)
const rangeResult = validateRangeComponent(quantityRangeComponent);
```

**What WON'T Work:**
```typescript
// ❌ These functions do NOT exist or are NOT exported
validateQuantityRange(component);  // Error: not exported (use validateRangeComponent)
validateVector(component);         // Error: returns { valid: true } without validation
validateMatrix(component);         // Error: returns { valid: true } without validation
validateGeometryData(component);   // Error: function not found
validateNilValues(component);      // Error: function not found
```

**Workaround for Missing Validators:**

```typescript
// For Range types, use the generic validator
import { validateRangeComponent } from 'ogc-client/csapi/validation';

// Works for QuantityRange, CountRange, TimeRange, CategoryRange
const result = validateRangeComponent(rangeComponent);

// For unsupported types, implement custom validation
function validateVectorManually(component: any): boolean {
  if (component.type !== 'Vector') return false;
  if (!component.referenceFrame) return false;
  if (!Array.isArray(component.coordinates)) return false;
  // Add more checks as needed
  return true;
}
```

---

## SensorML Validation System

**Location:** `src/ogc-api/csapi/validation/sensorml-validator.ts`  
**Test Count:** 13 tests  
**Code Coverage:** Not measured (no coverage report available)

### ✅ Implemented Validators (3 Functions)

**Process Validators:**
- `validateSensorMLProcess(process)` - Validates PhysicalSystem, PhysicalComponent, SimpleProcess, AggregateProcess
- `validateDeployment(deployment)` - Validates Deployment metadata
- `validateDerivedProperty(property)` - Validates derived property definitions

**What Each Validator Checks:**

✅ **Structural Validation:**
- Required properties present (`type`, `id`, `name`, etc.)
- Type-specific constraints (e.g., PhysicalSystem has `components`)
- Array structure validation (components, inputs, outputs)

✅ **Type Checking:**
- Process type validation (PhysicalSystem, PhysicalComponent, SimpleProcess, AggregateProcess)
- Nested object structure validation

✅ **Format Validation:**
- Custom format validators added to Ajv:
  - `uri` - Validates URIs (both URLs and URNs)
  - `iso-datetime` - Basic ISO 8601 date/time validation
  - `geojson-geometry` - Basic GeoJSON geometry structure check

✅ **Required Properties:**
- `type` field presence
- `id` field presence
- Type-specific required properties

### ❌ NOT Implemented (Despite Strong Claims)

**Schema-Based Validation:**
- ❌ Does **NOT** fetch OGC JSON schemas from `schemas.opengis.net`
- ❌ Does **NOT** validate against actual OGC JSON schemas
- ❌ Does **NOT** use Ajv for schema validation (Ajv is imported and configured but never used)
- ❌ Does **NOT** cache schemas (no schemas to cache)

**What the Code Actually Does:**

The `sensorml-validator.ts` file contains this revealing comment:

```typescript
async function initializeValidator(): Promise<Ajv> {
  // ...
  ajvInstance = new Ajv({
    strict: false,
    allErrors: true,
    verbose: true,
  });
  
  addFormats(ajvInstance);

  // In a real implementation, schemas would be fetched and cached
  // For now, we'll do basic structural validation  ← ACTUAL APPROACH
  schemasLoaded = true;
  
  return ajvInstance;
}
```

**Schema URLs Defined But Never Used:**
```typescript
export const SENSORML_SCHEMA_URLS = {
  PhysicalSystem: 'https://schemas.opengis.net/sensorML/3.0/json/physicalSystem.json',
  PhysicalComponent: 'https://schemas.opengis.net/sensorML/3.0/json/physicalComponent.json',
  // ... URLs exist but are NEVER fetched
};
```

**Why Functions Are Async:**
Functions are declared `async` but don't actually perform any asynchronous operations (no `await`, no network requests). This suggests the async nature was planned for schema fetching but never implemented.

### ⚠️ Important Distinctions

**What Documentation Claims:**
> "Async validation against OGC JSON schemas from schemas.opengis.net"  
> "JSON Schema compliance checking using Ajv"  
> "Schema caching for performance"

**What Actually Happens:**
- ✅ **Structural validation** with manual type checking
- ✅ **Required property enforcement**
- ✅ **Format validation** for URIs and dates
- ❌ **NO schema fetching**
- ❌ **NO Ajv validation** against schemas
- ❌ **NO schema caching** (nothing to cache)

**Practical Impact:**
The validators work and provide useful structural validation, but they do **NOT** guarantee strict OGC JSON Schema compliance. Subtle schema violations may not be caught.

### 📝 Usage Examples

**Valid Usage:**
```typescript
import { 
  validateSensorMLProcess,
  validateDeployment,
  validateDerivedProperty 
} from 'ogc-client/csapi/validation';

// Process validation (works for all process types)
const result = await validateSensorMLProcess(physicalSystem);
if (!result.valid) {
  console.error('Invalid process:', result.errors);
}

// Deployment validation
const deploymentResult = await validateDeployment(deployment);

// Property validation
const propertyResult = await validateDerivedProperty(property);
```

**What to Expect:**
```typescript
// ✅ Will catch:
- Missing required properties (type, id, name)
- Wrong process type
- Invalid URI formats
- Malformed nested structures

// ❌ May NOT catch:
- Subtle JSON Schema violations
- Properties not matching exact OGC schemas
- Complex schema constraints not manually implemented
- Additional properties not in schema
```

**Important Note:**
Functions are `async` but don't need to be `await`-ed in most cases since they perform no actual async operations:

```typescript
// This works, but the await is unnecessary
const result = await validateSensorMLProcess(process);

// This also works (though TypeScript may warn)
const result = validateSensorMLProcess(process);
```

---

## Summary Matrix

| Validation System | Implemented | Claimed But Missing | Approach |
|-------------------|-------------|---------------------|----------|
| **GeoJSON** | 21 validators (7 feature + 7 collection + 7 type guards) | Geometry validation, Link validation, Temporal validation, GeometryCollection support | Structural |
| **SWE Common** | 9 component validators + 3 constraint validators | 8 component validators (ranges as separate functions, abstract validators, geometry/nil validators), Required OGC property validation | Structural |
| **SensorML** | 3 process validators | OGC schema fetching, Ajv schema validation, Schema caching | Structural (NOT schema-based) |

**Overall Assessment:**
- ✅ **Core structural validation works** and is production-ready for basic use cases
- ⚠️ **Advanced validation features are limited** or missing
- ❌ **Schema-based validation is NOT implemented** despite documentation suggesting it is
- ✅ **Constraint validation (SWE Common) is excellent** and comprehensive

---

## Migration Guide

### If You Expected Schema-Based Validation

**What You Thought:**
> "The library validates against OGC JSON schemas fetched from schemas.opengis.net"

**Reality:**
The library uses structural validation, not schema-based validation.

**What This Means:**
- No network requests for schemas
- Faster validation (no async operations needed)
- Works offline
- May not catch all OGC specification violations

**Recommendation:**
If strict schema compliance is required, consider:
1. Using a separate JSON Schema validator library (like Ajv) with OGC schemas
2. Implementing additional validation checks
3. Testing against reference implementations

### If You Expected Advanced GeoJSON Validation

**What You Thought:**
> "The library validates geometries, links, and temporal data"

**Reality:**
Only basic GeoJSON structure and CSAPI-specific properties are validated.

**What This Means:**
- Geometry coordinates are NOT validated
- Links array is NOT validated
- ISO 8601 temporal formats are NOT validated
- GeometryCollection is NOT supported

**Recommendation:**
Implement custom validation for:
- Geometry coordinate validation (use a GeoJSON validation library)
- Link structure validation (check rel, href, type fields)
- Temporal format validation (use date parsing libraries)

### If You Expected All SWE Common Components

**What You Thought:**
> "The library validates all 24 SWE Common component types"

**Reality:**
Only 9 component validators are implemented, and 5 types return `{ valid: true }` without validation.

**What This Means:**
- Vector, Matrix, DataStream, DataChoice, Geometry: NO validation
- Range validators: Use generic `validateRangeComponent()` instead of type-specific functions
- Definition and label: NOT validated (despite being OGC-required)

**Recommendation:**
For unsupported types:
1. Implement custom validation logic
2. Use type guards to check structure
3. Consider testing against reference implementations

---

## Recommendations

### For Library Users

**DO:**
- ✅ Use validators for basic structural validation
- ✅ Rely on constraint validation (intervals, patterns, significant figures)
- ✅ Use type guards for type checking
- ✅ Implement additional validation for advanced features
- ✅ Test thoroughly with real data

**DON'T:**
- ❌ Assume schema-based validation is happening
- ❌ Rely solely on validators for production data quality
- ❌ Use functions that don't exist (check this doc first)
- ❌ Expect validation of geometries, links, or temporal data
- ❌ Assume all SWE Common types are validated

### For Library Developers

**High Priority:**
1. Correct all documentation claiming schema-based validation
2. Document which validators exist vs which are claimed
3. Add tests for collection validators (currently 0% coverage)
4. Test `validateObservationResult()` (currently 0% coverage)

**Medium Priority:**
1. Implement geometry validation (coordinates, types, GeometryCollection)
2. Implement link validation (structure, URL format)
3. Implement temporal validation (ISO 8601 format)
4. Implement missing SWE Common validators (Vector, Matrix, DataStream, DataChoice, Geometry)
5. Add definition/label validation per OGC 24-014

**Low Priority:**
1. Consider implementing actual schema-based validation (fetch from schemas.opengis.net)
2. Use Ajv for JSON Schema validation
3. Implement schema caching
4. Add deep recursive validation for aggregate SWE Common types

---

## Related Issues

- [Issue #12](https://github.com/Sam-Bolling/CSAPI-Live-Testing/issues/12) - GeoJSON validation discrepancies
- [Issue #14](https://github.com/Sam-Bolling/CSAPI-Live-Testing/issues/14) - SWE Common missing validators
- [Issue #15](https://github.com/Sam-Bolling/CSAPI-Live-Testing/issues/15) - SensorML structural validation approach
- [Issue #25](https://github.com/Sam-Bolling/CSAPI-Live-Testing/issues/25) - Correct GeoJSON coverage claim
- [Issue #26](https://github.com/Sam-Bolling/CSAPI-Live-Testing/issues/26) - Correct SWE Common coverage claim
- [Issue #27](https://github.com/Sam-Bolling/CSAPI-Live-Testing/issues/27) - Update validation capabilities documentation (this document)

---

## Version History

| Date | Version | Changes |
|------|---------|---------|
| 2026-01-28 | 1.0 | Initial comprehensive validation capabilities reference |

---

**Questions or Issues?**  
If you discover additional discrepancies between claimed and actual validation capabilities, please open an issue in the [CSAPI-Live-Testing](https://github.com/Sam-Bolling/CSAPI-Live-Testing) repository.
