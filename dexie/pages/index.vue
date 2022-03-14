<template>
  <Tutorial/>
</template>

<script>
import Dexie from 'dexie'

export default {
  mounted() {
    const db = new Dexie('dexie')
    db.version(4).stores({
      people: 'id,name,age,func'
    })
    
    db.open()
      .then(() => {
        db.people.add({name: 'John', age: 42})
        db.people.add({name: 'Mary', age: 35})
        db.people.add({name: 'Peter', age: 27})
        return db.people.toArray()
      })
  },
}
</script>
