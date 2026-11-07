<script>
    let product = $state("Producto")
    let units = $state(1)
    let meters_pu = $state(80)
    let price = $state()
    let price_pm = $state()
    let items = $state([])
    let warning = $state()

    function calc() {
        if (units && meters_pu && price) {
            price_pm = (price / (units * meters_pu)).toFixed(2)
        }
        warning = null
    }

    function add() {
        if (!product || !units || !meters_pu || !price) {
            warning = "Por favor complete todos los campos"
            return
        }
        warning = null
        items = [...items, { product, units, meters_pu, price, price_pm }]
        product = ""
        units = 1
        meters_pu = 80
        price = ""
        price_pm = ""
    }
</script>
<p>
    <a href="/">Volver</a>
</p>
<form>
    <ul>
        <li>
            <label for="product">Producto</label>
            <input id="product" type="text" bind:value={product}/>
        </li>
        <li>
            <label for="unidades">Unidades</label>
            <input id="unidades" type="text" bind:value={units} on:input={calc}/>
        </li>
        <li>
            <label for="metros_pu">Metros por unidad</label>
            <input id="metros_pu" type="text" bind:value={meters_pu} on:input={calc}/>
        </li>
        <li>
            <label for="precio">Precio</label>
            <input id="precio" type="text" bind:value={price} on:input={calc}/>
        </li>    
    </ul>
</form>
<p>Precio por metro: {price_pm}</p>
<button on:click={add}>Agregar</button>
<p>{warning}</p>

<table>
    <thead>
        <tr>
            <th>Producto</th>
            <th>Unidades</th>
            <th>Metros por unidad</th>
            <th>Precio</th>
            <th>Precio por metro</th>
        </tr>
    </thead>
    <tbody>
        {#each items as item}
            <tr>
                <td>{item.product}</td>
                <td>{item.units}</td>
                <td>{item.meters_pu}</td>
                <td>{item.price}</td>
                <td>{item.price_pm}</td>
            </tr>
        {/each}
    </tbody>
</table>
    