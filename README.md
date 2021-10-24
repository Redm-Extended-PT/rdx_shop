# rdx_shop

## Requirements
- [rdx_menu_default](https://github.com/Redm-Extended-PT/rdx_menu_default)

## Download & Installation

- Download https://github.com/Redm-Extended-PT/rdx_shop
- Put it in the `[rdx]` directory

## Installation
- Add this to your `server.cfg`:

```
ensure rdx_shop
```

## Usage Add more items
```lua
openlojamenu = function()
	RDX.UI.Menu.Open(
		'default', GetCurrentResourceName(), 'lojas',
		{
            title  = 'loja' ,
            align = 'center',
			elements = {
				{label = "Pão $3", type = "slider", value = 1, min = 1, max = 1, price = 3, item = "bread"},
				{label = "Água $3", type = "slider", value = 1, min = 1, max = 1, price = 3, item = "water"},
				--{label = "Milho $2", type = "slider", value = 1, min = 1, max = 1, price = 2, item = "milho"},
            }
		},
		function(data, menu)
			local name = data.current.item
			local amount = data.current.value
			local money = data.current.value * data.current.price

			TriggerServerEvent('rdx_lojaseller:buy', name, amount, money)
        end,
        function(data, menu)
			menu.close()
        end
	)
end