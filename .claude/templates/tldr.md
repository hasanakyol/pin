# TLDR: [Feature Name]

## Quick Summary

[2-3 sentences describing what this feature does and why it exists]

## Concrete Artifacts

### Database Schema (from database.md)
```sql
-- Key tables created
CREATE TABLE [table_name] (
  id UUID PRIMARY KEY,
  [key_fields]: [types]
);
```

### API Endpoints (from api.md)
- `[METHOD] /path`: [Description]
- `[METHOD] /path`: [Description]

### Frontend Components (from frontend.md - if applicable)
- **[ComponentName]**: [Purpose and key props]
- **[ComponentName]**: [Purpose and key props]

## Key Components

- **[Component 1]**: [Purpose]
- **[Component 2]**: [Purpose]
- **[Component 3]**: [Purpose]

## Key Functions/Methods

- `functionName()`: [What it does]
- `className.methodName()`: [What it does]

## Files Created/Modified

- `path/to/file.ext`: [Purpose]
- `path/to/file.ext`: [Purpose]

## Shared Resources

### Provided to Other Features

- **Interface/Utility Name**: `src/shared/interfaces/[Name]`
  - Purpose: [What it does]
  - Contract: [Interface or API]
  - Used by: [Features]

### Consumed from Other Features

- **Interface/Utility Name**: `src/shared/interfaces/[Name]`
  - Purpose: [What it does]
  - Provider: [Feature]
  - Contract: [Interface or API]

## Dependencies on Other Features

- **[Feature-001]**: Uses [specific interface/component]
- **[Feature-002]**: Shares [specific utility/model]

## External Dependencies

- [Library/Package]: [Why used]
- [Library/Package]: [Why used]

## Testing

- Test Coverage (diff‑aware): [X]% on changed files
- Test Files: `path/to/tests`
- Key Test Scenarios: [Main scenarios]

## Observability Summary

- Logging: structure, correlation IDs, log points
- Error Taxonomy: applied categories and handling
- Metrics/Tracing: key signals

## Configuration

- Environment Variables: [List]
- Config Files: [List]

## Security Considerations

- [Measure 1]
- [Measure 2]

## Performance Notes

- [Consideration 1]
- [Consideration 2]

## Integration Points

- **Frontend**: [Integration]
- **Backend**: [Integration]
- **Database**: [Usage]

## Quickstart & Usage

- **How to run locally**: [Instructions for setting up and running the feature]
- **Example API Usage**:
  ```bash
  # Example showing how to use this feature via API call
  curl -X POST /api/v1/[endpoint] -d '{"field": "value"}'
  ```
- **Frontend Usage** (if applicable):
  ```jsx
  <ComponentName prop="value" onAction={handleAction} />
  ```
- **Key Outputs**: [Description of expected outputs for the examples]

## Next Steps

- Recommended next feature: [Feature name]
- Potential enhancements: [Ideas]

## Version & Migration

- Version Bump: [MAJOR.MINOR.BUILD]
- Breaking Changes: [Yes/No]
- Migration Notes: [Required steps]
- Parallel Contract Tests: [Old vs New validated]

## Concrete Artifact Sources

- **Database specifications**: `features/[###-feature]/database.md`
- **API specifications**: `features/[###-feature]/api.md`  
- **Frontend specifications**: `features/[###-feature]/frontend.md` (if applicable)
- **High-level design**: `features/[###-feature]/design.md`

---

Based on PINDEX Constitution v1.0.0
