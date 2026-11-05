# Warehouse tools

Small Python utilities for warehouse order and shipping workflows.

Run the tests with `python3 -m unittest discover -s tests -v`.

## Shipping

`shipping_quote(weight_kg, zone, service="standard")` returns a delivery quote
in US dollars. Zones are `local` and `regional`; weights must be positive.

| Service    | Local base | Regional base | Surcharge |
|------------|-----------|---------------|-----------|
| `standard` | $5.00     | $8.00         | –         |
| `express`  | $5.00     | $8.00         | +$7.00    |

All services add $1.50 per kg on top of the base. Unknown zones or service
levels raise `ValueError`.

### CLI

```
python -m warehouse.cli <weight_kg> <zone> [--service {standard,express}]
```

Examples:

```bash
# Standard (default)
python -m warehouse.cli 2 local           # $8.00

# Express
python -m warehouse.cli 2 local --service express    # $15.00
python -m warehouse.cli 2 regional --service express # $18.00
```
