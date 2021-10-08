<template>
  <div>
    <h1>
      {{ home.title }}
    </h1>

    <div style="display:flex;">
      <img
        v-for="image in home.images"
        :key="image"
        :src="image"
        alt="home"
        height="200px"
        width="200px"
        style="padding: .6rem 1rem;"
      />
    </div>
    ${{ home.pricePerNight }} <br />
    {{ home.reviewvalue }} <br />
    {{ home.location.address }}, {{ home.location.city }},
    {{ home.location.state }}, {{ home.location.country }} <br />
    {{ home.guests }}, {{ home.bedrooms }}, {{ home.beds }},
    {{ home.bathrooms }} <br />
    {{ home.description }} <br />

    <div id="map" style="width: 250px;height:200px"></div>
  </div>
</template>

<script>
import homes from "~/data/homes.json";
import mapboxgl from "mapbox-gl";
import MapBoxGeoCoder from "@mapbox/mapbox-gl-geocoder";
import "@mapbox/mapbox-gl-geocoder/dist/mapbox-gl-geocoder.css";
export default {
  head() {
    return {
      title: this.home.title,
      link: [
        {
          rel: "stylesheet",
          href: "https://api.mapbox.com/mapbox-gl-js/v2.4.1/mapbox-gl.css"
        }
      ]
    };
  },
  data() {
    return {
      home: {},
      accessToken:
        "pk.eyJ1Ijoia3VyYW1hMTEiLCJhIjoiY2t0ODBxY2U0MHhlaTJ3bzd1Ym11ZXEyNyJ9.xg11fBF7OP144dd7_0tfhg"
    };
  },
  created() {
    const home = homes.find(home => home.objectID == this.$route.params.id);
    this.home = home;
  },
  mounted() {
    this.createMap();
  },
  methods: {
    async createMap() {
      try {
        mapboxgl.accessToken = this.accessToken;
        const map = new mapboxgl.Map({
          container: "map",
          style: "mapbox://styles/mapbox/streets-v11",
          center: [this.home._geoloc.lng, this.home._geoloc.lat],
          zoom: 14
        });
        const marker = new mapboxgl.Marker({
          draggable: true,
          color: "#D80739"
        })
          .setLngLat([this.home._geoloc.lng, this.home._geoloc.lat])
          .addTo(map);
      } catch (error) {
        console.log(error);
      }
    }
  }
};
</script>
