<template>
  <div class="table">
    <h1>{{ msg }}</h1>
    <b-table striped hover :items="buildings"
             :fields="fields"
             :select-mode="selectMode"
             responsive="sm"
             ref="selectableTable"
             selectable
             @row-selected="onRowSelected"
    ></b-table>
  </div>
</template>

<script>
export default {
  name: 'BuildingList',
  props: {
    msg: String
  },
  data() {
    return {
      fields: [
        {
          key: 'type',
          label: 'Type',
          sortable: false
        },
        {
          key: 'id',
          label: 'ID',
          sortable: true
        },
        {
          key: 'name',
          label: 'Name',
          sortable: true,
        },
        {
          key: 'x',
          label: 'X coordinate',
          sortable: true
        },
        {
          key: 'y',
          label: 'Y coordinate',
          sortable: true
        }
      ],
      buildings: [
        {
          "type": "Building",
          "id": "B1",
          "name": "General hospital",
          "x": 1300,
          "y": 560
        },
        {
          "type": "Building",
          "id": "B2",
          "name": "Firehall",
          "x": -350,
          "y": 1100
        },
        {
          "type": "Building",
          "id": "B3",
          "name": "University",
          "x": -890,
          "y": -1300
        },
        {
          "type": "Building",
          "id": "B4",
          "name": "Central library",
          "x": 470,
          "y": 1010
        },
        {
          "type": "Building",
          "id": "B5",
          "name": "Secondary school",
          "x": 1550,
          "y": 850
        },
        {
          "type": "Building",
          "id": "B6",
          "name": "Primary school",
          "x": 1450,
          "y": 950
        },
        {
          "type": "Building",
          "id": "B7",
          "name": "City Hall",
          "x": -600,
          "y": 200
        },
      ],
      towers: [
        {
          "type": "Cell Tower",
          "id": "C1",
          "name": "Bell NW",
          "x": 2200,
          "y": 1720
        },
        {
          "type": "Cell Tower",
          "id": "C2",
          "name": "Bell NE",
          "x": -1090,
          "y": 1400
        },
        {
          "type": "Cell Tower",
          "id": "C3",
          "name": "Bell SW",
          "x": 760,
          "y": -1360
        },
        {
          "type": "Cell Tower",
          "id": "C4",
          "name": "Bell SE",
          "x": -1410,
          "y": -450
        },
        {
          "type": "Cell Tower",
          "id": "C5",
          "name": "Rogers NW1",
          "x": 2300,
          "y": 1710
        },
        {
          "type": "Cell Tower",
          "id": "C6",
          "name": "Rogers NW2",
          "x": 50,
          "y": 2080
        },
        {
          "type": "Cell Tower",
          "id": "C7",
          "name": "Rogers SE",
          "x": -1410,
          "y": -450
        },
        {
          "type": "Cell Tower",
          "id": "C8",
          "name": "Freedom SW",
          "x": 1100,
          "y": -1200
        },
        {
          "type": "Cell Tower",
          "id": "C9",
          "name": "Freedom NE",
          "x": -1090,
          "y": 1400
        },
        {
          "type": "Cell Tower",
          "id": "C10",
          "name": "TELUS SE1",
          "x": -1740,
          "y": -50
        },
        {
          "type": "Cell Tower",
          "id": "C11",
          "name": "TELUS SE2",
          "x": -2300,
          "y": -350
        }
      ],
      selectMode: 'single',
      filteredArray: [],
    }
  },
  methods: {
    onRowSelected(items) {
      let xBuilding = items[0].x
      let yBuilding = items[0].y
      let result = this.towers.map(tower => {
        let xTower = tower.x
        let yTower = tower.y
        let distance = Math.sqrt(Math.pow(xTower - xBuilding, 2) + Math.pow(yTower - yBuilding, 2)).toFixed(2)
        return {
          "type": tower.type,
          "id": tower.id,
          "name": tower.name,
          "x": tower.x,
          "y": tower.y,
          "distance": distance
        }
      }).sort((a, b) => a.distance - b.distance)
      this.filteredArray = result
      this.$bvModal.msgBoxOk(`${this.filteredArray[0].name} is the closest to the building.
      Coordinates: X:${this.filteredArray[0].x} Y:${this.filteredArray[0].y}
      Distance: ${this.filteredArray[0].distance}`, {
        title: 'The closest cell tower:',
        size: 'lg',
        buttonSize: 'lg',
        okVariant: 'success',
        headerClass: 'p-2 border-bottom-0',
        footerClass: 'p-2 border-top-0',
        centered: true
      })
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
