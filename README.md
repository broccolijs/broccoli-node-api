# `broccoli-node-api`

TypeScript types for the [Broccoli Node Api](https://github.com/broccolijs/broccoli/blob/master/docs/node-api.md)

- [`broccoli-node-api`](#broccoli-node-api)
  - [Exports](#exports)
    - [Node](#node)
    - [FeatureSet](#featureset)
    - [NodeInfo](#nodeinfo)
    - [NodeType](#nodetype)
    - [NodeInfoCommon](#nodeinfocommon)
    - [TransformNodeInfo](#transformnodeinfo)
    - [CallbackObject](#callbackobject)
    - [SourceNodeInfo](#sourcenodeinfo)

## Exports

### Node

```ts
interface Node {
  __broccoliFeatures__: FeatureSet;
  __broccoliGetInfo__: (builderFeatures: FeatureSet) => NodeInfo;
}
```

[Node Documentation](https://github.com/broccolijs/broccoli/blob/master/docs/node-api.md#part-2-node-api-specification)

---

### FeatureSet

```ts
interface FeatureSet {
  [feature: string]: boolean;
}
```

---

### NodeInfo

```ts
type NodeInfo = SourceNodeInfo | TransformNodeInfo;
```

[NodeInfo Documentation](https://github.com/broccolijs/broccoli/blob/master/docs/node-api.md#the-nodeinfo-object)

---

### NodeType

```ts
type NodeType = "source" | "transform";
```

---

### NodeInfoCommon

```ts
interface NodeInfoCommon<T extends NodeType> {
  nodeType: T;
  name: string;
  annotation: string | null | undefined;
  instantiationStack: string;
}
```

---

### TransformNodeInfo

```ts
interface TransformNodeInfo extends NodeInfoCommon<"transform"> {
  inputNodes: Node[];
  setup(inputPaths: string[], outputPath: string, cachePath: string): void;
  getCallbackObject(): CallbackObject;
  persistentOutput: boolean;
  needsCache: boolean;
}
```

[TransformNodeInfo Documentation](https://github.com/broccolijs/broccoli/blob/master/docs/node-api.md#transform-nodes)

---

### CallbackObject

```ts
interface CallbackObject {
  build(): Promise<void>;
}
```

---

### SourceNodeInfo

```ts
interface SourceNodeInfo extends NodeInfoCommon<"source"> {
  sourceDirectory: string;
  watched: boolean;
}
```

[SourceNodeInfo Documentation](https://github.com/broccolijs/broccoli/blob/master/docs/node-api.md#source-nodes)
