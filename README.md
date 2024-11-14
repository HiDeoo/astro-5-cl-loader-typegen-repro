# astro-5-cl-loader-typegen-repro

## Steps to reproduce

1. Clone this repository
1. Run `pnpm install`
1. Run `pnpm dev` to generate the type definitions
1. Check the generated types in `.astro/content.d.ts`

The `docs` content collection is using a loader but gets the old/compat type generated with a `slug` and a `render()` properties.

```ts
type ContentEntryMap = {
  docs: {
    "guide.md": {
      id: "guide.md";
      slug: "guide";
      body: string;
      collection: "docs";
      data: InferEntrySchema<"docs">;
    } & { render(): Render[".md"] };
    "test.md": {
      id: "test.md";
      slug: "test";
      body: string;
      collection: "docs";
      data: InferEntrySchema<"docs">;
    } & { render(): Render[".md"] };
  };
};
```

Moving the `docs` collection to `src/data/docs/` and updating the `base` in the `src/content/config.ts` file generates the expected type.
