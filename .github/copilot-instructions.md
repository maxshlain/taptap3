# COPILOT EDITS OPERATIONAL GUIDELINES
                
## PRIME DIRECTIVE
	Avoid working on more than one file at a time.
	Multiple simultaneous edits to a file will cause corruption.
	Be chatting and teach about what you are doing while coding.

## LARGE FILE & COMPLEX CHANGE PROTOCOL

### MANDATORY PLANNING PHASE
	When working with large files (>300 lines) or complex changes:
		1. ALWAYS start by creating a detailed plan BEFORE making any edits
            2. Your plan MUST include:
                   - All functions/sections that need modification
                   - The order in which changes should be applied
                   - Dependencies between changes
                   - Estimated number of separate edits required
                
            3. Format your plan as:
## PROPOSED EDIT PLAN
	Working with: [filename]
	Total planned edits: [number]

### MAKING EDITS
	- Focus on one conceptual change at a time
	- Show clear "before" and "after" snippets when proposing changes
	- Include concise explanations of what changed and why
	- Always check if the edit maintains the project's coding style

### Edit sequence:
	1. [First specific change] - Purpose: [why]
	2. [Second specific change] - Purpose: [why]
	3. Do you approve this plan? I'll proceed with Edit [number] after your confirmation.
	4. WAIT for explicit user confirmation before making ANY edits when user ok edit [number]
            
### EXECUTION PHASE
	- After each individual edit, clearly indicate progress:
		"✅ Completed edit [#] of [total]. Ready for next edit?"
	- If you discover additional needed changes during editing:
	- STOP and update the plan
	- Get approval before continuing
                
### REFACTORING GUIDANCE
	When refactoring large files:
	- Break work into logical, independently functional chunks
	- Ensure each intermediate state maintains functionality
	- Consider temporary duplication as a valid interim step
	- Always indicate the refactoring pattern being applied
    
# GitHub Copilot Instructions - Python Best Practices

Follow these guidelines when generating Python code for modern software development with Python.

## Project Structure
When creating or organizing Python projects:
- Use src-layout with `src/your_package_name/` structure
- Place tests in `tests/` directory parallel to `src/`
- Keep configuration in `config/` or use environment variables
- Store requirements in `requirements.txt` or `pyproject.toml`

## Code Style and Formatting
Always generate code that follows these standards:
- Apply Black code formatting standards
- Use isort conventions for import sorting
- Follow PEP 8 naming conventions:
  - `snake_case` for functions and variables
  - `PascalCase` for classes
  - `UPPER_CASE` for constants
- Keep maximum line length at 88 characters (Black default)
- Prefer absolute imports over relative imports

## Type Hints
Include comprehensive type hints in all generated code:
- Add type hints for all function parameters and return values
- Import types from `typing` module when needed
- Use `Optional[Type]` instead of `Type | None` for compatibility
- Use `TypeVar` for generic types
- Suggest custom types in `types.py` for complex type definitions
- Use `Protocol` for duck typing interfaces

## Testing Code
Generate comprehensive test suites:
- Use pytest as the testing framework
- Write tests for all application routes
- Include pytest-cov for coverage reporting
- Create reusable pytest fixtures
- Use pytest-mock for proper mocking
- Test error scenarios and edge cases

## Error Handling
Create robust error handling:
- Define custom exception classes for specific errors
- Use appropriate try-except block structures
- Implement comprehensive logging for debugging
- Return user-friendly error responses
- Handle edge cases gracefully
- Provide meaningful error messages

## Documentation Standards
Include proper documentation:
- Use Google-style docstrings for all functions and classes
- Document all public APIs comprehensively
- Generate inline comments for complex logic
- Create clear function and class descriptions
- Document environment setup requirements

## Development Environment
When suggesting development setup:
- Use virtual environments (venv) for isolation
- Configure pre-commit hooks for code quality
- Follow Git workflow best practices
- Implement semantic versioning
- Set up proper CI/CD pipelines
- Configure appropriate logging levels

## Dependency Management
Handle dependencies properly:
- Pin specific dependency versions in requirements
- Separate production and development dependencies
- Use appropriate package version constraints
- Suggest regular dependency updates
- Include security vulnerability checks

## Code Generation Guidelines
When generating Python code:
1. Always include appropriate imports at the top
2. Add comprehensive docstrings and comments
3. Include error handling and validation
4. Use type hints consistently
5. Follow the established project structure
6. Implement security best practices by default
7. Generate tests alongside main code when appropriate
8. Include logging statements for debugging
9. Use environment variables for configuration
10. Follow the DRY (Don't Repeat Yourself) principle

Remember to adapt these guidelines based on the specific project context and requirements while maintaining consistency with these established patterns.