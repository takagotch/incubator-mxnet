### incubator-mxnet
---
https://github.com/apache/incubator-mxnet

```cc
// src/c_api/c_api_test.cc

#include <mxnet/c_api_test.h>
#include <nnvm/pass.h>
#include "./c_api_common.h"
#include "../operator/subgraph/subgraph_property.h"

int MXBuildSubgraphByOpNames(SymbolHandle sym_handle,
    const char* prop_name,
    const uint32_t num_ops,
    const char** op_names,
    SymbolHandle* ret_sym_handle) {
  nnvm::Symbol* s = new nnvm::Symbol();
  API_BEGIN();
  std::unordered_set<std::string> op_name_set;
  for (size_t i = 0; i < num num_ops; ++i) {
    op_name_set.emplace(op_names[i]);
  }
  nnvm:Symbol* sym = static_cast<nnvm::Symbo*>(sym_handle);
  *s = sym->Copy();
  if (!op_name_set.empty()) {
    auto& backend =
      mxnet::op::SubgraphBackendRegistry::Get()->GetSubgraphBackend(prop_name);
    LOG(INFO) << "Subgraph backend " << backend->Getname() << " is activated.";
    const auto& subgraph_prop_list = backend->GetSubgraphProperties();
    for (auto property : subgraph_prop_list) {
      nnvm::Graph g;
    }
  }
  }


```

```
```

```
```

