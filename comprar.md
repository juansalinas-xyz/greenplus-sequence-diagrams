sequenceDiagram
participant p as Person
participant f as front
participant b as backend
participant db as Mongo
participant gp as payment
participant bc as blockchain

p-->>+f:POST: /buy/{projectId}
note over p,f: body: purchageCart
    f-->>+b:POST: /buy/{projectId}
    note over f,b: body: purchageCart
    b-->>+gp: POST: /Payment/aprove
    gp-->>-b: return Response
    alt Response.ok
        loop forEach purchageCart.product
            b-->>+db: searchProductById
            db-->-b: retuen Product
            b-->>+bc: transferAsset
            note over b,bc: product.tokenId, amount
            note over b,bc: walletIdFrom, walletIdTo
            bc-->>-b: return ok
        end
    end
    b-->>-f: return purchageInfo
f-->>-p: return purchageInfo