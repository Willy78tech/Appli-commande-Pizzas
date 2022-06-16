<template>
  <div class="row">
    <div class="col-md-8 bg-light mt-3 mx-3">
      <form action="#" method="post" class="p-2 ">
        <div class="row">
          <div class="col-md-6">
            <div class="form-group">
              <input
                type="text"
                class="form-control"
                id="name"
                name="name"
                placeholder="Nom"
                required
              />
            </div>
          </div>
          <div class="col-md-6">
            <div class="form-group">
              <input
                type="email"
                class="form-control"
                id="email"
                name="email"
                placeholder="Courriel"
                required
              />
            </div>
          </div>
        </div>
        <div class="form-group mt-2">
          <textarea
            class="form-control"
            name="message"
            id="message"
            rows="4"
            placeholder="Message"
            required
          ></textarea>
        </div>
        <div class="form-group mt-2">
          <button type="submit" class="btn btn-primary">
            Soumettre
          </button>
        </div>
      </form>
    </div>
  </div>
</template>


<style></style>
