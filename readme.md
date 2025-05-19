# TipTap React Render

[![npm](https://img.shields.io/npm/v/@abidmiah128/tiptap-react-render.svg?style=flat)](https://www.npmjs.com/package/@abidmiah128/tiptap-react-render)
[![npm](https://img.shields.io/npm/dt/@abidmiah128/tiptap-react-render)](https://www.npmjs.com/package/@abidmiah128/tiptap-react-render)

This library renders [TipTap](https://tiptap.dev/) JSON payloads in React clients without embedding the editor.

### Installation

```sh
# npm
npm install @abidmiah128/tiptap-react-render

# yarn
yarn add @abidmiah128/tiptap-react-render
```

### Usage

```typescript
// handle the document
const doc: NodeHandler = (props) => <>{props.children}</>;

// handle a paragraph
const paragraph: NodeHandler = (props) => {
  return <p style={props.node.attrs}>{props.children}</p>;
};

// handle text
const text: NodeHandler = (props) => {
  const { node } = props;
  let content = <span>{node.text}</span>;

  return content;
};
// handle an image
const img: NodeHandler = (props) => {
  const { src, alt, title } = props.node;
  return <img src={src} alt={alt} title={title} />;
};

// create a handlers wrapper
const handlers: NodeHandlers = {
  doc: doc,
  text: text,
  paragraph: paragraph,
  img: img,
};

// sample tip tap data
const data = {
  type: 'doc',
  content: [
    {
      type: 'paragraph',
      content: [
        {
          type: 'text',
          text: 'Hey, try to select some text here. There will popup a menu for selecting some inline styles. Remember: you have full control about content and styling of this menu.',
        },
      ],
    },
  ],
};
// render it!
const rendered = <TipTapRender handlers={handlers} node={data} />;
```

### Why?

Many folks render TipTap rich text by embedding the TipTap editor in a "read-only" mode. However, if you don't want to add TipTap as a dependency (or, like us, you're using a platform that can't support it like React Native), then this is a simple, lightweight tool for mapping TipTap nodes to presentation components!

We were inspired by Contentful's [rich-text-react-renderer](https://github.com/contentful/rich-text/tree/master/packages/rich-text-react-renderer) tool, so we built a similar one for TipTap payloads!

This repo was scaffolded using the [@alexeagleson/template-react-component-library](https://github.com/alexeagleson/template-react-component-library)
