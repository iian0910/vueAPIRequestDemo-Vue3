<template>
  <div class="container">
    <div class="row" v-for="(item, index) in apiData.data" :key="index">{{item.Add}}</div>

    <div class="row">
      <div class="col-md-4" v-for="(item, index) in apiData.data" :key="index">
        <div class="card">
          <div class="card-head">
            <div class="zoneTeg">{{item.Zone}}</div>
            <img class="picture" :style="{ backgroundImage: 'url(' + item.Picture1 + ')' }">
          </div>
          <div class="card-body">
            <h3 class="card-title">{{item.Name}}</h3>
            <ul class="list-group list-group-flush">
              <li class="list-group-item card-info mb-1" v-if="item.Ticketinfo === '免費參觀'">
                <i class="fa fa-ticket card-info-icon"></i>{{item.Ticketinfo}}
              </li>
              <li class="list-group-item card-info mb-1" v-if="item.Ticketinfo !== '免費參觀'">
                <i class="fa fa-ticket card-info-icon"></i>尚無資訊
              </li>
              <li class="list-group-item card-info mb-1">
                <i class="fa fa-map-marker card-info-icon"></i>{{item.Add}}
              </li>
              <li class="list-group-item card-info">
                <i class="fa fa-phone card-info-icon"></i>{{item.Tel}}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { computed, onMounted, reactive } from 'vue'
import axios from 'axios'

export default ({

  setup () {
    // data
    const apiData = reactive({
      data: []
    })

    // computed
    const newAdd = computed(() => {
      return apiData.data.forEach((travelData: TravelData) => {
        if (travelData.Add) {
          travelData.Add = travelData.Add.substring(6)
          console.log('travelData', travelData)
        }
      })
    })

    // methods
    function getData () {
      const api = 'https://raw.githubusercontent.com/hexschool/KCGTravel/master/datastore_search.json'
      axios.get(api)
        .then((res) => {
          apiData.data = res.data.result.records
          console.log('apiData.data', apiData.data)
        })
        .catch((err) => {
          console.log('err', err)
        })
    }

    // lifecycle
    onMounted(() => {
      getData()
    })

    return {
      apiData,
      newAdd
    }
  }
})

export interface TravelData {
  Add: string;
  Changetime: string;
  Class1: string;
  Class2: string;
  Description: string;
  Gov: string;
  Id: string;
  Level: string;
  Name: string;
  Opentime: string;
  Parkinginfo_px: string;
  Parkinginfo_py: string;
  Picdescribe1: string;
  Picture1: string;
  Px: string;
  Py: string;
  Remarks: string;
  Tel: string;
  Ticketinfo: string;
  Toldescribe: string;
  Travellinginfo: string;
  Website: string;
  Zone: string;
}
</script>

<style scoped lang="scss">
@import "~bootstrap/scss/bootstrap";
  .card-head {
    position: relative;
    .zoneTeg {
      position: absolute;
      bottom: 5px;
      right: 5px;
      padding: 5px 15px;
      border-radius: 5px;
      background-color: $info;
      color: white;
      font-weight: bold;
    }
  }

  .card-title {
    font-size: 20px;
    font-weight: bold;
  }

  .picture {
    width: 100%;
    height: 0;
    padding-top: calc(100% * 4 / 6);
    display: block;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
  }

  .card-info {
    padding: 0;
    margin: 0;
    border: 0;
  }

  .card-info-icon {
    margin-right: 8px;
    width: 16px;
    height: 16px;
    color: $info;
    text-align: center;
  }
</style>
