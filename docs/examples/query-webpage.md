```python
from zytron.artifacts import BaseArtifact
from zytron.drivers import LocalVectorStoreDriver
from zytron.loaders import WebLoader


vector_store = LocalVectorStoreDriver()

[
    vector_store.upsert_text_artifact(a, namespace="zytron")
    for a in WebLoader(max_tokens=100).load("https://www.zytron.ai")
]

results = vector_store.query(
    "creativity",
    count=3,
    namespace="zytron"
)

values = [BaseArtifact.from_json(r.meta["artifact"]).value for r in results]

print("\n\n".join(values))
```