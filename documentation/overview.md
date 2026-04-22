# API Overview


# include/Side.h
### (no methods)
- Defines `enum class Side { Buy, Sell }`. **Type:** enum
---


# include/OrderType.h
### (no methods)
- Defines `enum class OrderType { GoodTillCancel, FillAndKill, GoodForDay, Market }`. **Type:** enum
---


# include/Usings.h
### (no methods)
- Defines aliases used across the codebase: `Price`, `Quantity`, `OrderId`, `orderIds`. **Type:** type aliases
---


# include/Constants.h
### (no methods)
- Declares `struct Constants { ... }` (fields not shown in retrieved content). **Type:** struct / constants container
---


# include/LevelInfo.h
### (no methods)
- Defines `struct LevelInfo { Price price; Quantity quantity; }`. **Type:** struct (data-only)

### (no methods) `LevelInfos`
- `using LevelInfos = std::vector<LevelInfo>;`. **Type:** type alias
---


# include/TradeInfo.h
### (no methods)
- Defines `struct TradeInfo { OrderId orderId_; Price price_; Quantity Quantity_; }`. **Type:** struct (data-only)
---


# include/Trade.h
### Trade(...)
- Creates a `Trade` containing bid-side and ask-side `TradeInfo` for one execution. **Type:** public constructor

### GetBidTrade()
- Returns the bid-side `TradeInfo`. **Type:** public getter (const)

### GetAskTrade()
- Returns the ask-side `TradeInfo`. **Type:** public getter (const)

### (no methods) `Trades`
- `using Trades = std::vector<Trade>;` (multiple executions can result from one add). **Type:** type alias
---


# include/Order.h
### Order(...)
- Constructs an order and initializes fill-tracking quantities. **Type:** public constructor

### GetOrderId()
- Returns the order ID. **Type:** public getter (const)

### GetSide()
- Returns the side (`Buy`/`Sell`). **Type:** public getter (const)

### GetPrice()
- Returns the limit price. **Type:** public getter (const)

### GetOrderType()
- Returns the order type/time-in-force. **Type:** public getter (const)

### GetInitialQuantity()
- Returns the original quantity. **Type:** public getter (const)

### GetRemainingQuantity()
- Returns unfilled quantity remaining. **Type:** public getter (const)

### GetFilledQuantity()
- Returns filled quantity (`initial - remaining`). **Type:** public computed getter (const)

### isFilled()
- Returns whether the order is fully filled. **Type:** public predicate (const)

### Fill(quantity)
- Fills `quantity` from the remaining quantity; throws if it would overfill. **Type:** public mutator

### (no methods) `OrderPointer`
- `using OrderPointer = std::shared_ptr<Order>;`. **Type:** type alias

### (no methods) `OrderPointers`
- `using OrderPointers = std::list<OrderPointer>;` (stable iterators). **Type:** type alias
---


# include/OrderModify.h
### OrderModify(...)
- Constructs a modify request (id + new side/price/quantity). **Type:** public constructor

### GetOrderId()
- Returns which order ID to modify. **Type:** public getter (const)

### GetPrice()
- Returns the replacement price. **Type:** public getter (const)

### GetSide()
- Returns the replacement side. **Type:** public getter (const)

### GetQuantity()
- Returns the replacement quantity. **Type:** public getter (const)

### ToOrderPointer(type)
- Builds a new `OrderPointer` using this modify request and the provided `OrderType`. **Type:** public converter / factory (const)

---


# include/OrderbookLevelInfos.h
### OrderbookLevelInfos(...)
- Constructs a container for bid/ask `LevelInfos` snapshots. **Type:** public constructor

### GetBids()
- Returns the bid-side level infos. **Type:** public getter (const)

### GetAsks()
- Returns the ask-side level infos. **Type:** public getter (const)
---


# include/Orderbook.h
### Addorder(order)
- Adds an order (skips duplicates), then matches and returns resulting `Trades`; rejects `FillAndKill` if no immediate match is possible. **Type:** public command / entrypoint

### CancelOrder(orderId)
- Cancels an order by id (no-op if not found) and removes it from internal structures. **Type:** public command

### CanMatch(side, price)
- Checks whether an incoming order at `price` can match the current best price on the opposite side. **Type:** private helper (const)

### MatchOrders()
- Matches orders while best bid >= best ask, performs fills, removes filled orders/empty levels, returns all executions. **Type:** private helper / matching engine
---


# src/Orderbook.cpp
### (no methods)
- Currently contains only includes; no function definitions present. **Type:** translation unit stub
---


# src/main.cpp
### main()
- Program entry point; currently returns `0` and does not exercise the order book. **Type:** free function / executable entrypoint