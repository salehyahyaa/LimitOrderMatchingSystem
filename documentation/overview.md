# Documentation Overview – Method Reference


# INCLUDE
## Orderbook.h

### Addorder(order)
- Adds a new order (ignores duplicate IDs), inserts it into bids/asks, then matches and returns the resulting trades. Also short-circuits `FillAndKill` if it can’t immediately match. **Type:** public command

### CancelOrder(orderId)
- Cancels an order by ID (no-op if not found) and removes it from the internal book structures. **Type:** public command

### CanMatch(side, price)
- Checks whether an incoming order at `price` can match the current best price on the opposite side. **Type:** private helper (const)

### MatchOrders()
- Core matching loop: while best bid >= best ask, fills quantities, removes filled orders/empty levels, and returns all executions. **Type:** private helper


## Order.h

### Order(orderType, orderId, side, price, quantity)
- Creates an order and initializes fill tracking (initial and remaining quantities). **Type:** public constructor

### GetOrderId()
- Returns the order’s unique ID. **Type:** public getter (const)

### GetSide()
- Returns `Buy` or `Sell`. **Type:** public getter (const)

### GetPrice()
- Returns the limit price. **Type:** public getter (const)

### GetOrderType()
- Returns the time-in-force / order type. **Type:** public getter (const)

### GetInitialQuantity()
- Returns the original submitted quantity. **Type:** public getter (const)

### GetRemainingQuantity()
- Returns how much is still open/unfilled. **Type:** public getter (const)

### GetFilledQuantity()
- Returns how much has been filled (`initial - remaining`). **Type:** public computed getter (const)

### isFilled()
- Returns whether the order is fully filled (remaining == 0). **Type:** public predicate (const)

### Fill(quantity)
- Decreases remaining quantity by `quantity`; throws if `quantity` exceeds remaining quantity. **Type:** public mutator


## OrderModify.h

### OrderModify(orderId, side, price, quantity)
- Creates a “modify request” containing replacement values for an existing order. **Type:** public constructor

### GetOrderId()
- Returns the target order ID. **Type:** public getter (const)

### GetSide()
- Returns the replacement side. **Type:** public getter (const)

### GetPrice()
- Returns the replacement price. **Type:** public getter (const)

### GetQuantity()
- Returns the replacement quantity. **Type:** public getter (const)

### ToOrderPointer(type)
- Converts the modify request into a new `OrderPointer` with the given `OrderType` (useful for cancel+replace). **Type:** public factory (const)


## Trade.h

### Trade(bidTrade, askTrade)
- Creates a trade object holding bid-side and ask-side execution info. **Type:** public constructor

### GetBidTrade()
- Returns bid-side execution details. **Type:** public getter (const)

### GetAskTrade()
- Returns ask-side execution details. **Type:** public getter (const)


## OrderbookLevelInfos.h

### OrderbookLevelInfos(bids, asks)
- Creates a container holding bid/ask `LevelInfos` snapshots. **Type:** public constructor

### GetBids()
- Returns bid-side level infos. **Type:** public getter (const)

### GetAsks()
- Returns ask-side level infos. **Type:** public getter (const)


## Side.h

### (no methods)
- `enum class Side { Buy, Sell }`. **Type:** enum


## OrderType.h

### (no methods)
- `enum class OrderType { GoodTillCancel, FillAndKill, GoodForDay, Market }`. **Type:** enum


## Usings.h

### (no methods)
- Aliases: `Price`, `Quantity`, `OrderId`, `orderIds`. **Type:** type aliases


## LevelInfo.h

### (no methods)
- `struct LevelInfo { Price price; Quantity quantity; }` and `using LevelInfos = std::vector<LevelInfo>`. **Type:** struct + alias


## TradeInfo.h

### (no methods)
- `struct TradeInfo { OrderId orderId_; Price price_; Quantity Quantity_; }`. **Type:** struct (data-only)


## Constants.h

### (no methods)
- `struct Constants { ... }` (fields not visible in retrieved snippet). **Type:** struct / constants containe