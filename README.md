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
      g.outputs = s->outputs;
      property->SetAttr("graph", g);
      property->SetAttr("op_names", op_name_set);
      g.attrs["subgraph_property"] = std::make_shared<nnvm::any>(property);
      g = nnvm::ApplyPass(std::move(g), "BuildSubgraph");
      property->RemoveAttr("graph");
      g.attrs.erase("subgraph_property");
      s->outputs = g.outputs;
    }
  }
  *ret_sym_handle = s;
  API_END_HANDLE_ERROR(delete s);
}

int MXSetSubgraphPropertyOpNames(const char* prop_name,
    const uint32_t num_ops,
    const char** op_name) {
  API_BEGIN();
  std::unordered_set<> op_name_set;
  for (size_t i = 0; i < num_ops; ++i) {
    op_name_set.emplace(op_names[i]);
  }
  (*mxnet::op::SubgraphPropertyOpNameSet::Get())[prop_name] = op_name_set;
  API_END();
}

int MXRemoveSubgraphPropertyOpNames(const char* prop_name) {
  API_BEGIN();
  mxnet::op::SubgraphPropetyOpNameSet::Get()->erase(prop_name);
  API_END();
}


```

```
```

```
```

