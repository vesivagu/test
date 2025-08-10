You are an expert Angular developer and testing specialist. 
Write a complete Jest test file for the provided Angular source file. 
Ensure:
- 100% coverage for statements, branches, functions, and lines.
- Test public and private methods via public API.
- Mock dependencies, services, and Angular modules.
- Use Angular TestBed for components and services.
- Include positive and negative test scenarios.
- Follow Arrange-Act-Assert pattern.
- Do not skip tests; make them passable without external APIs.

Source file:
[Paste the file content here]

# Angular 19 – Ready-to-Use Jest Test Case Prompts

## 1. Universal Angular 19 Jest Test Prompt
You are a senior Angular 19 developer and Jest testing expert. 
Write a complete `.spec.ts` test file for the given Angular code.
Requirements:
- Use Jest as the test runner.
- Achieve 100% coverage for statements, branches, functions, and lines.
- For components: use Angular TestBed, test creation, Inputs, Outputs, DOM rendering, event bindings, change detection, lifecycle hooks.
- For services: mock dependencies, test success and error flows.
- For pipes: test transformation with edge cases and invalid values.
- For guards/resolvers: test allowed and blocked routes.
- Use Arrange-Act-Assert pattern.
- Include both positive and negative scenarios.
- Do not skip tests and ensure they run without external APIs.

Source code:
[Paste your Angular code here]

---

## 2. Component-Specific Prompt
You are an Angular 19 + Jest expert.
Generate a `.spec.ts` file for this component with:
- Angular TestBed configuration.
- Unit tests for creation, Input property binding, Output event emission.
- DOM queries using `fixture.nativeElement` and `DebugElement`.
- Lifecycle hooks (`ngOnInit`, `ngOnChanges`, `ngOnDestroy`).
- Simulated user interactions (click, input, form submission).
- Positive and negative test cases.
- Full coverage without hitting external APIs.

Component code:
[Paste component code]

---

## 3. Service-Specific Prompt
You are a senior Angular 19 QA engineer.
Generate a Jest unit test file for this service:
- Mock all dependencies using `jest.fn()` or `jest.mock()`.
- Test all methods with success and failure scenarios.
- Handle Observables with `of()`, `throwError()`, and `async/await` for Promises.
- Ensure 100% branch coverage.
- Verify interactions with mocked dependencies.
- Avoid real HTTP calls by mocking HttpClient.

Service code:
[Paste service code]

---

## 4. Pipe-Specific Prompt
You are an Angular 19 testing expert.
Generate a Jest `.spec.ts` for this pipe:
- Test transformation with normal, boundary, and invalid inputs.
- Cover all conditional branches.
- Ensure idempotent transformation (same input twice yields same output).
- Avoid external dependencies.

Pipe code:
[Paste pipe code]

---

## 5. Guard or Resolver Prompt
You are an Angular 19 + Jest testing expert.
Write a Jest test file for this Angular route guard/resolver:
- Mock Router, ActivatedRouteSnapshot, and RouterStateSnapshot.
- Test allowed and blocked navigation.
- Test async and sync return types (Observable, Promise, boolean).
- Cover all branches including error cases.
- Ensure no skipped tests.

Guard/Resolver code:
[Paste guard/resolver code]

---

## 6. Full Project Bulk Coverage Prompt
You are an Angular 19 + Jest testing specialist.
For every TypeScript file in my project except `*.spec.ts`:
- Generate a Jest test file.
- Match folder structure in `__tests__/` directory.
- For components: test creation, Inputs/Outputs, DOM events, lifecycle hooks.
- For services: mock dependencies and cover all methods.
- For pipes: cover normal and edge cases.
- For guards/resolvers: cover allowed and blocked routes.
- Ensure >95% statement and branch coverage.
- Avoid real API calls; mock everything.
List the tested files, then provide the test code.
