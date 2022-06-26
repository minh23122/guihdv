<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">Home</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item active">
            <a class="nav-link" href="#"
              >Home <span class="sr-only">(current)</span></a
            >
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">sản phẩm</a>
          </li>
        </ul>
      </div>
    </nav>
    <div class="card-body">
      <div class="row">
        <div class="col-2" v-for="post in posts" :key="post.id">
          <!-- <nuxt-link to="/posts/1"> -->
          <div class="box-post border p-2 position-relative">
            <div class="image">
              <img src="~/assets/images/logo.png" class="w-100" alt="" />
            </div>
            <p class="line-3">
              {{ post.title }}
            </p>
            <button
              type="button"
              class="btn btn-primary"
              data-toggle="modal"
              data-target="#exampleModal"
            >
              Thanh toán
            </button>
          </div>
          <!-- </nuxt-link> -->
        </div>
      </div>
    </div>

    <!-- Modal -->
    <div
      class="modal fade"
      id="exampleModal"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Thanh toán</h5>
            <button
              type="button"
              class="close"
              data-dismiss="modal"
              aria-label="Close"
            >
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <form>
              <div class="form-group">
                <label for="exampleFormControlSelect2">Đơn vị vận chuyển</label>
                <select class="form-control" id="exampleFormControlSelect2">
                  <option>Tiki</option>
                  <option>Giao hàng nhanh</option>
                  <option>Shopee</option>
                  <option>Giao hàng tiết kiệm</option>
                </select>
              </div>
              <div class="form-group">
                <label for="exampleFormControlTextarea1">Ghi chú</label>
                <textarea
                  class="form-control"
                  id="exampleFormControlTextarea1"
                  rows="3"
                ></textarea>
              </div>
            </form>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-dismiss="modal"
            >
              Close
            </button>
            <button type="button" class="btn btn-primary" @click="payment">
              Xác nhận
            </button>
          </div>
        </div>
      </div>
    </div>
    <script src="https://code.jquery.com/jquery-3.2.1.slim.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.12.9/dist/umd/popper.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.0.0/dist/js/bootstrap.min.js"></script>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "IndexPage",
  async asyncData({ $axios, params }) {
    const posts = await $axios.$get(
      `https://jsonplaceholder.typicode.com/posts?_limit=5`
    );
    console.log(posts);
    return { posts };
  },

  methods: {
    async payment({ $axios }) {
      const posts = await axios.post(`http://localhost:8097/process`, {
        products: [
          {
            id: 4,
          },
        ],
        shipment: {
          id: 2,
          price: 70000.0,
        },
      });
      $('#exampleModal').hide();
      alert('success');
    },
  },
};
</script>
