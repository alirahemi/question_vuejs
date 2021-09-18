<template>
    <div>
  <b-navbar toggleable="lg" type="dark" variant="info" class="p-2">
    <b-navbar-brand href="#" class="">Question & Answer</b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
        <b-nav-item href="#">correct Answers {{ correctCount }}/{{totalCount}}</b-nav-item>
      </b-navbar-nav>

      <!-- Right aligned nav items -->
      
    </b-collapse>
  </b-navbar>
</div>
</template>

<script>
export default {
  props: {
    correctCount: Number,
    totalCount: Number
  }
}
</script>