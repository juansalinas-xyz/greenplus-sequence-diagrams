sequenceDiagram
participant p as Person
participant f as front
participant b as backend
participant db as Mongo

p-->>+f: GET:/projects/{idProject}
    f-->>+b: GET:/projects/{idProject}
        b-->>+db: searchById
        db-->>-b: return project
    b-->>-f: return project
f-->>-p: return Project

p-->>+f: GET:/projects/products/info
    f-->>+b: GET:/projects/products/info
        b-->>+db: searchProductsByIdProject
        b-->>+b: mapProductInfo()
        db-->>-b: return ProductsInfo
    b-->>-f: return ProductsInfo
f-->>-p: return ProductsInfo