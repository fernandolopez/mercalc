<script>
    let product = $state("Producto")
    let units = $state(1)
    let unit_amount = $state(1)
    let price = $state()
    let price_pl = $state()
    let items = $state([])
    let warning = $state()
    let mode = $state("mass")
    let unit_singular = $state("kilo")
    let unit_plural = $state("kilos")

    function clear(full = false) {
        product = "Producto"
        units = 1
        price = ""
        price_pl = ""
        if (mode === "lineal") {
            unit_amount = 100
        }
        else {
            unit_amount = 1
        }
        if (full) {
            items = []
        }
    }

    function calc() {
        if (units && unit_amount && price) {
            price_pl = (price / (units * unit_amount)).toFixed(2)
        }
        warning = null
    }

    function add() {
        if (!product || !units || !unit_amount || !price) {
            warning = "Por favor complete todos los campos"
            return
        }
        warning = null
        items = [...items, { product, units, unit_amount, price, price_pl }]
        clear()
    }

    function set_mode() {
        if (mode === "mass") {
            unit_singular = "kilo"
            unit_plural = "kilos"
        } else if (mode === "lineal") {
            unit_singular = "metro"
            unit_plural = "metros"
        } else if (mode === "volume") {
            unit_singular = "litro"
            unit_plural = "litros"
        }
        clear(true)
    }

    function title_case(str) {
        return str.charAt(0).toUpperCase() + str.slice(1)
    }
</script>

<form>
    <select bind:value={mode} on:change={() => set_mode()}>
        <option value="mass" selected>Por peso</option>
        <option value="lineal">Por metro</option>
        <option value="volume">Volumen</option>
    </select>
    <ul>
        <li>
            <label for="product">Producto</label>
            <input id="product" type="text" bind:value={product}/>
        </li>
        <li>
            <label for="units">Unidades</label>
            <input id="units" type="text" bind:value={units} on:input={calc}/>
        </li>
        <li>
            <label for="unit_amount">{title_case(unit_plural)} por unidad</label>
            <input id="unit_amount" type="text" bind:value={unit_amount} on:input={calc}/>
        </li>
        <li>
            <label for="price">Precio</label>
            <input id="price" type="text" bind:value={price} on:input={calc}/>
        </li>    
    </ul>
</form>
<p>Precio por {unit_singular}: {price_pl}</p>
<button on:click={add}>Agregar</button>
<button on:click={() => clear(true)}>Limpiar</button>
<p>{warning}</p>

<table>
    <thead>
        <tr>
            <th>Producto</th>
            <th>Unidades</th>
            <th>{title_case(unit_plural)} por unidad</th>
            <th>Precio</th>
            <th>Precio por {unit_singular}</th>
        </tr>
    </thead>
    <tbody>
        {#each items as item}
            <tr>
                <td>{item.product}</td>
                <td>{item.units}</td>
                <td>{item.unit_amount}</td>
                <td>{item.price}</td>
                <td>{item.price_pl}</td>
            </tr>
        {/each}
    </tbody>
</table>
    