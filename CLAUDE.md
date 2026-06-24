# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm start          # dev server at http://localhost:4200 (hot reload)
npm run build      # production build → dist/
npm run watch      # dev build in watch mode
npm test           # run unit tests with Vitest via Angular CLI
```

Scaffolding new Angular artifacts:
```bash
ng generate component component-name
ng generate service service-name
ng generate --help   # full list of schematics
```

## Architecture

Angular 22 standalone component app (no NgModules). Entry point is `src/main.ts` → bootstraps `App` from `src/app/app.ts`.

- **Standalone components**: every component declares its own `imports` array; no shared `NgModule` wrappers.
- **Routing**: `src/app/app.routes.ts` exports `routes: Routes` (currently empty); registered via `provideRouter` in `src/app/app.config.ts`.
- **Signals**: state is managed with Angular signals (`signal()`), not RxJS `BehaviorSubject`.
- **Styles**: SCSS throughout; component styles are inline via `styleUrl`; global styles in `src/styles.scss`.
- **Component selector prefix**: `lfds-*` (configured in `angular.json`).

## Formatting

Prettier is configured (`.prettierrc`): 100-char print width, single quotes, Angular HTML parser for `.html` files. Run `npx prettier --write .` to format.

## Testing

Tests use Vitest (not Karma/Jest) via `@angular/build:unit-test`. Test files live alongside source as `*.spec.ts`. The `TestBed` API is used for component tests.
