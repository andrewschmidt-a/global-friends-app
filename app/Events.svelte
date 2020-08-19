<page>
    <actionBar title="Svelte Native App | Events" />
    {#if auth.loggedIn}
     <tabs tabsPosition="top">
				<tabStrip>
          {#each events as event}
						<tabStripItem title={event.title} />
	        {/each}
				</tabStrip>

      {#each events as event}
        <tabContentItem>
        <stackLayout backgroundColor="#3c495e" style="text-align:center;">
          <label text="Time:" height="20" fontWeight="bold"/>
          <label text="{event.time}" height="20" />
          <label text="RSVP:" height="30" fontWeight="bold" />
          <listPicker height="50" items="{event.venues.map(t=> t.title)}" selectedIndex="0" />
        </stackLayout>
        </tabContentItem>
      {/each}

		</tabs>
    {/if}
</page>

<script>
    export let firebase;
    var dateFormat = require('dateformat');
    var now = new Date();

    console.log(firebase)
    export let auth;
    let events = [
      {
        "title": "English Class",
        "time": dateFormat(now, "dddd, mmmm dS, yyyy, h:MM:ss TT"),
        "venues":[
          {
            "id": null,
            "title": "Not Going",
            "capacity": Infinity,
            "participants":[]
          },
          {
            "id": 1,
            "title": "House 1",
            "capacity": 20,
            "participants":[]
          },
          {
            "id": 2,
            "title": "House 2",
            "capacity": 20,
            "participants":[]
          }
        ]
      },
      {
        "title": "Movie Night",
        "time": Date.now(),
        "venues":[
          {
            "id": 1,
            "title": "House 1",
            "capacity": 20,
            "participants":[]
          }
        ]
      },
      {
        "title": "BBQ",
        "time": Date.now(),
        "venues":[
          {
            "id": 1,
            "title": "House 1",
            "capacity": 20,
            "participants":[]
          }
        ]
      }
    ];
    
</script>

<style>
    .info .fas {
        color: #3A53FF;
    }
    .info {
        font-size: 20;
    }
</style>
