<script>
    import { resolve } from '$app/paths';
    let product = $state("Producto")
    let units = $state(1)
    let litters = $state(1)
    let price = $state()
    let price_pl = $state()
    let items = $state([])
    let warning = $state()

    function calc() {
        if (units && litters && price) {
            price_pl = (price / (units * litters)).toFixed(2)
        }
        warning = null
    }

    function add() {
        if (!product || !units || !litters || !price) {
            warning = "Por favor complete todos los campos"
            return
        }
        warning = null
        items = [...items, { product, units, litters, price, price_pl }]
        product = ""
        units = 1
        litters = 1
        price = ""
        price_pl = ""
    }
</script>
<p>
    <a href={resolve('/')}>Volver</a>
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
            <label for="litros">Litros por unidad</label>
            <input id="litros" type="text" bind:value={litters} on:input={calc}/>
        </li>
        <li>
            <label for="precio">Precio</label>
            <input id="precio" type="text" bind:value={price} on:input={calc}/>
        </li>    
    </ul>
</form>
<p>Precio por litro: {price_pl}</p>
<button on:click={add}>Agregar</button>
<p>{warning}</p>

<table>
    <thead>
        <tr>
            <th>Producto</th>
            <th>Unidades</th>
            <th>Litros por unidad</th>
            <th>Precio</th>
            <th>Precio por litro</th>
        </tr>
    </thead>
    <tbody>
        {#each items as item}
            <tr>
                <td>{item.product}</td>
                <td>{item.units}</td>
                <td>{item.litters}</td>
                <td>{item.price}</td>
                <td>{item.price_pl}</td>
            </tr>
        {/each}
    </tbody>
</table>
    