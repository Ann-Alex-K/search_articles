<template>
  <div class="article">
    <h1>Try it!</h1>
    <div class="search">
      <input
        type="text"
        v-model.trim="searchResult"
        placeholder="Write the title of the article"
        @keyup="saveSearch"
      />
    </div>
    <p v-if="noResults">No results</p>
    <ul>
      <li v-for="article in searchText" :key="article.id">
        <h4>{{ article.title }}</h4>
        <p>{{ article.text }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "ArticleSearch",
  data() {
    return {
      searchResult: "",
      textArr: [
        {
          id: 1,
          title: "New York City. Part 1",
          text: `New York - city and port located at the mouth of the Hudson River, southeastern New York state, northeastern U.S. New York City is the centre of the largest urban agglomeration in the United States. It occupies Manhattan and Staten islands, the western end of Long Island, a portion of the mainland, and various islands in New York Harbor and Long Island Sound. Its urban area extends into neighbouring parts of New York, New Jersey, and Connecticut.

New York City is an ethnic melting pot where the most dramatic cultural contrasts are commonplace. It is among the most geographically and demographically complex of world cities, its economy one of the most diverse, and its cultural scene among the richest and most variegated.

A brief treatment of New York City follows. For full treatment, see New York City.

The city consists of five boroughs (Manhattan, Brooklyn, Queens, the Bronx, and Staten Island [formerly Richmond]), which correspond to five counties of New York state (New York, Kings, Queens, Bronx, and Richmond, respectively). All are located near the point where the Hudson River empties into Upper New York Bay of the Atlantic Ocean. The city's only land boundaries are Westchester county on the north and Nassau county on Long Island to the east. The city's waterfront is used for shipping and recreation.`,
        },
        {
          id: 2,
          title: "Sydney city. Part 1",
          text: `Сity, capital of the state of New South Wales, Australia. Located on Australia's southeastern coast, Sydney is a major port in the South Pacific and is noted for its beautiful harbour. The city was established as a penal colony in the late 18th century and had become a major trading centre even before the first pioneers pushed inland. It is now the largest metropolitan area in Australia.

A brief treatment of Sydney follows. For full treatment, see Sydney.

The metropolitan area of Sydney stretches from the Blue Mountains in the west to the Pacific Ocean in the east and from the Hawkesbury River in the north to south of Botany Bay. The city itself was built on the low hills surrounding the harbour.

Sydney's climate is temperate, with a mean temperature in February, the warmest month, of 72 F (22 C); the coolest month, July, averages 54 F (12 C). Rainfall averages 45 inches (1,140 mm) annually, and much of it occurs during the summer months.`,
        },
        {
          id: 3,
          title: "London city, Capital of the United Kingdom.",
          text: `London - city, capital of the United Kingdom and the centre of the Commonwealth. It lies astride the River Thames in southeastern England, 50 miles (80 km) from the river's estuary on the North Sea. The city was once the industrial, commercial, and political hub of a wealthy and extensive empire; it continues to be the United Kingdom's main centre of population, commerce, and culture.

A brief treatment of London follows. For full treatment (including a map), see London.

The chalk basin within which London is built is filled with younger sediments including solid rock, sands, clays, terraced pebble gravels, and Thames alluvium. The climate within the basin is relatively mild, with January to July mean temperatures ranging from 37.4 to 72.5 F (3 to 22.5 C); rainfall amounts to 21 inches (533 mm) a year.`,
        },
        {
          id: 4,
          title: "New York City. Part 2",
          text: `Ethnic pockets abound throughout Manhattan, from black and Spanish Harlem in the north, to the various enclaves of the Lower East Side such as Little Italy and Chinatown. New York City also has large numbers of Italians, Irish, Puerto Ricans, and West Indians, as well as the largest Jewish population of any city in the world. This ethnic and racial mix is the result of the waves of immigration that the city has absorbed during its history. The Statue of Liberty, located on Liberty Island off Manhattan, has long stood as a symbol of refuge and opportunity.

New York City is a centre of world trade and finance, communications, art and entertainment, and fashion. The city is the financial capital of the United States and holds the headquarters of many of the world's largest corporations. Wall Street in Manhattan is home to the nation's largest stock exchange and is the headquarters of the country's largest brokerage firms. With the headquarters of the nation's television and radio networks and the main offices of the largest advertising agencies, New York City is the heart of the mass media in the United States. Printing and publishing are also of great importance, and most of the nation's major publishing houses are based in midtown Manhattan. The city's economic life also depends on the great diversity of its numerous small businesses and manufacturing establishments.
`,
        },
        {
          id: 5,
          title: "New York City. Part 3",
          text: `The artists of New York City exhibit in a wide variety of forms, ranging from traditional crafts to the most avant-garde work, flavoured by complex blends of ethnic and national influences. Theatrical arts and entertainment are also widespread: Broadway is the synonym for musical comedies and legitimate drama; Carnegie Hall is one of the most famous concert halls in the world; and Lincoln Center for the Performing Arts is the home of the Metropolitan Opera, the New York City Opera, the New York Philharmonic, and the New York City Ballet. Though the importance of Broadway has declined, theatre is very much alive in the more venturesome Off-Broadway and off-off-Broadway productions. The city has numerous motion-picture theatres, among which are many revival and foreign-film houses.

The New York Public Library is one of the best research libraries in the world. Most famous among the city's many museums are the Metropolitan Museum of Art, the Museum of Modern Art, the Solomon R. Guggenheim Museum, the Whitney Museum of American Art, and the American Museum of Natural History. Many lesser known museums house special collections. The city's extensive system of public parks includes Central Park in Manhattan.

`,
        },
        {
          id: 6,
          title: "Sydney city. Part 2",
          text: `About one-third of Sydney's workforce is engaged in manufacturing. No single industry predominates, though oil refining has grown in importance. The government sector is also economically important, as is the port. A second port has been developed in Botany Bay.

Sydney is widely known both for its water sports and recreational facilities and for its cultural life. The universities of Sydney and New South Wales are located there, as is Macquarie University. The world-renowned Sydney Opera House, set on a promontory southeast of the Harbour Bridge, is a major centre for the performing arts, with theatres and recording, concert, and exhibition halls. It is the home of the Sydney Symphony Orchestra, the Australian Opera, dance and theatre companies, and a library.

Rapid development of suburban Sydney and the absence of major highways that bypass the city have caused a persistent transport problem that is only partially mitigated by commuter ferry boats, an underground railway, and extensive metropolitan bus service. Sydney (Kingsford Smith) Airport is on the northern shore of Botany Bay. Area city, 5 square miles (13 square km); metropolitan area, 4,790 square miles (12,407 square km). Pop. (1986) city, 86,311; (1991) city, 3,097,956; (1994 est.) metropolitan area, 3,738,500.`,
        },
      ],
    };
  },
  computed: {
    searchText() {
      return this.textArr.filter((el) => {
        return el.title.toLowerCase().includes(this.searchResult);
      });
    },
    noResults() {
      return this.searchText.length === 0;
    },
  },
  methods: {
    saveSearch() {
      this.$router.push({
        name: "article",
        query: { search: this.searchResult },
      });
    },
  },
  created() {
    this.searchResult = this.$route.query.search;
  },
};
</script>

<style>
input {
  width: 37%;
  border: 3px solid #00b4cc;
  padding: 5px;
  height: 20px;
  border-radius: 5px;
  outline: none;
}
input:focus {
  background-color: #e6f6f7;
}

ul li p {
  text-align: left;
  padding-right: 20px;
}
ul li h4 {
  margin-left: 75px;
  font-weight: bold;
  padding-top: 12px;
  text-align: left;
}
</style>