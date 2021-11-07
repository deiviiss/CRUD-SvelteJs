<script>
  import { v4 } from "uuid";
  import Noty from "noty";

  //css noty
  import "noty/lib/noty.css";
  import "noty/lib/themes/sunset.css";

  let products = [
    {
      id: v4(),
      name: "Lenovo",
      description: "Laptop Lenovo",
      category: "Laptops",
      imageURL:
        "data:image/jpeg;base64,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",
    },
    {
      id: v4(),
      name: "Razer",
      description: "Mouse Razer",
      category: "perepherials",
      imageURL:
        "data:image/jpeg;base64,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",
    },
  ];

  let product = {
    id: "",
    name: "",
    description: "",
    category: "",
    imageURL: "",
  };

  let statusEdit = false;

  const addProduct = () => {
    const newProduct = {
      id: v4(),
      name: product.name,
      description: product.description,
      category: product.category,
      imageURL: product.imageURL,
    };

    products = products.concat(newProduct);

    cleanProduct();

    console.log(products);
  };

  const cleanProduct = () => {
    product = {
      id: "",
      name: "",
      description: "",
      category: "",
      imageURL: "",
    };
  };

  const onSubmitHandler = (e) => {
    // e.preventDefault();
    if (!statusEdit) {
      addProduct();
    } else {
      updateProduct();
    }
  };

  const updateProduct = () => {
    let updatedProduct = {
      name: product.name,
      description: product.description,
      category: product.category,
      imageURL: product.imageURL,
    };

    const productIndex = products.findIndex((p) => p.id === product.id);
    products[productIndex] = updatedProduct;
    cleanProduct();
    statusEdit = false;

    new Noty({
      theme: "sunset",
      type: "success",
      timeout: 3000,
      // layout: "bottomRight",
      text: "Product update successfully",
    }).show();
  };

  const deleteProduct = (id) => {
    products = products.filter((product) => product.id !== id);
  };

  const editProduct = (productEdit) => {
    product = productEdit;
    statusEdit = true;
    console.log(product);
  };
</script>

<main>
  <div class="container p-4">
    <div class="row">
      <div class="col-md-6">
        {#each products as product}
          <div class="card mt-2">
            <div class="row">
              <div class="col-md-4">
                {#if !product.imageURL}
                  <img
                    src="./images/no-product.png"
                    alt=""
                    class="img-fluid p-2"
                  />
                {:else}
                  <img src={product.imageURL} alt="" class="img-fluid p-2" />
                {/if}
              </div>
              <div class="col-md-8">
                <div class="card-body">
                  <h5><strong>{product.name}</strong></h5>
                  <span> <small>{product.category}</small> </span>
                  <p class="card-text">
                    {product.description}
                  </p>
                  <button
                    class="btn btn-danger"
                    on:click={deleteProduct(product.id)}>Delete</button
                  >
                  <button
                    class="btn btn-secondary"
                    on:click={editProduct(product)}>Edit</button
                  >
                </div>
              </div>
            </div>
          </div>
        {/each}
      </div>

      <div class="col-md-6">
        <div class="card">
          <div class="card-body">
            <form on:submit|preventDefault={onSubmitHandler}>
              <div class="form-group">
                <input
                  bind:value={product.name}
                  type="text"
                  placeholder="Product name"
                  class="form-control"
                />
              </div>

              <div class="form-group">
                <textarea
                  bind:value={product.description}
                  name=""
                  id="product-description"
                  cols=""
                  rows="3"
                  class="form-control"
                />
              </div>

              <div class="form-group">
                <input
                  bind:value={product.imageURL}
                  type="url"
                  name=""
                  id="product-img-url"
                  placeholder="https://"
                  class="form-control"
                />
              </div>

              <div class="form-group">
                <select
                  bind:value={product.category}
                  name=""
                  id="category"
                  class="form-control"
                >
                  <option selected disabled>Select a Category</option>
                  <option value="laptops">Laptops</option>
                  <option value="peripherials">Peripherials</option>
                  <option value="servers">Servers</option>
                </select>
              </div>

              {#if !statusEdit}
                <button class="btn btn-primary"> Saved</button>
              {:else}
                <button class="btn btn-primary"> Update</button>{/if}
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</main>

<style>
</style>
