
<template>
  <main>
    <!-- PROGRESSION -->
    <div v-if="currentIndex != 0" class="progress-bar-container">
      <div class="progress-bar" :style="{width: `${percentageOfProgress}`}">
      <span class="percentage">
        {{ percentageOfProgress }}
      </span>
      </div>
    </div>

    <!-- CONTENT -->
    <transition name="fade" @after-enter="scrollToTop">
    <div v-if="contentStory" class="content">
      <StoryView :content="contentStory[currentIndex]"/>
      <div v-if="currentIndex === contentStory.length - 1 ">Resultat: 
        <div  style="min-height: 100px; display: block;" v-for="(result, index) in results" :key="index">
          <br>
          <p>
            {{ result.question }}
          </p>
          <p>
            {{ result.response }}
          </p>
          <br>
          <hr>
        </div>
      </div>

      <!-- ACTIONS -->
      <div class="btn-container">
        <button title="Séléctioner" :class="`btn btn-response-${index + 1}`" v-for="(button, index) in contentStory[currentIndex].response" :key="index" @click="showNextContent(index)"><span v-if="currentIndex > 0">{{ index + 1 }}/ </span>{{ button }}</button>
      </div>
      <button title="Retour" class="btn-back" v-if="currentIndex !== 0" @click="showPreviousContent">&lt; Précédent</button>
    </div>
  </transition>
  </main>
</template>


<script setup lang="ts">
import { ref, onMounted, onUpdated } from 'vue';
import StoryView from '@/components/StoryView.vue';
import type { TContentStory } from '@/types/global';

const currentIndex = ref<number>(0);
const results = ref();

const contentStory= ref<TContentStory[]>([
  {
  title: 'Présentation du jeu',
  content: `Marc est cadre dans une grande entreprise. Bien que le succès soit au rendez-vous, il ne se sent pas heureux, il subit sa vie et se sent prisonnier d’une routine étouffante. Ce matin, Marc ressent une lourdeur dans sa poitrine, une sensation familière de mécontentement qui l'envahit dès qu'il pose le pied dans la grisaille matinale de sa ville du Nord. Assis dans le bus, il regarde par la fenêtre ruisselante de pluie les rues qui défilent, grises et monotones, reflétant parfaitement son état d'esprit.
    Au moment de quitter son siège car l’arrêt où il descend comme chaque jour de semaine depuis des années est proche, Marc remarque un petit livre abandonné sur le siège à côté de lui. Intrigué, il le ramasse et découvre qu'il s'agit d'un vieux carnet à la couverture usée. Mais à l'intérieur, les pages vierges attendent d'être remplies de mots, de pensées, de rêves peut-être.
    Une étincelle de curiosité s'allume dans les yeux de Marc. Il n'a jamais été du genre à tenir un journal, mais quelque chose dans ce carnet lui parle. Il décide de l'emporter avec lui, un geste anodin qui semble pourtant marquer le début d'un changement.
    Le soir, après sa journée de travail routinière, alors qu'il monte à bord de son bus, Marc sent une légère bouffée d'espoir l'envahir. Peut-être que ce petit carnet sera le catalyseur dont il a besoin pour échapper à la monotonie de sa vie. Ce n'est qu'un début, mais déjà, il se sent un peu moins prisonnier de sa routine étouffante.
    Dans les chapitres suivants, aidez Marc à transformer les croyances limitantes qui l'empêchent de se libérer de cette routine qui ne correspond pas à ses aspirations.`,
    response: [`ok, c’est parti!`]
  },
  {
    title: 'Chapitre 1 : Les Rêves Abandonnés',
    content: `Ce soir, alors que Marc explore son passé avec un regard critique, des souvenirs refont surface, teintés d' amertume. Il se remémore avec regret les aspirations qu'il avait autrefois, celles qui ne se sont jamais concrétisées. Parmi elles, le rêve d'exercer un métier atypique qui le passionnait, loin des sentiers battus du monde de l'entreprise. Marc voulait devenir photographe professionnel, explorant les horizons créatifs et capturant la beauté du monde à travers son objectif. 
      Au fir et à mesure qu’il noircit les pages de son carnet, il se souvient que ce rêve, pourtant si vivant dans son esprit, a été étouffé par une croyance limitante insidieuse : celle que le succès et la sécurité ne peuvent être trouvés que dans la voie conventionnelle. Convaincu qu'il devait suivre le chemin tracé par la société, Marc a abandonné son rêve, reléguant ses aspirations les plus profondes au second plan.
      Après avoir pris conscience de cela, une lueur d'espoir anime son regard...
      Quelle croyance aidante pourrait lui redonner confiance en lui, lui permettant de croire qu'il est encore possible de poursuivre son rêve aujourd'hui ?`,
    response:[
      `"Le succès et la sécurité sont le fruit de la persévérance et de l'authenticité dans la poursuite de mes aspirations, même en dehors des sentiers battus"`,
      `"Le succès et la sécurité sont le fruit de la persévérance et de l'authenticité dans la poursuite de mes aspirations, même en dehors des sentiers battus"`,
      `"Le succès et la sécurité sont le fruit de la persévérance et de l'authenticité dans la poursuite de mes aspirations, même en dehors des sentiers battus"`,
      `"Le succès et la sécurité sont le fruit de la persévérance et de l'authenticité dans la poursuite de mes aspirations, même en dehors des sentiers battus"`,
    ]
  },
  {
    title: 'Chapitre 2 : Le poids des jugements',
    content: `Le lendemain soir, alors que toute la journée il a repensé à son rêve professionnel, il n’avait qu’une obsession : se retrouver seul face à son petit carnet !
      Son dîner englouti en vitesse, il s’installe avec un stylo et replonge un peu plus en avant dans ses souvenirs. Une expérience marquante surgit dans sa mémoire : celle où il avait envisagé de changer de carrière pour poursuivre sa passion, mais a été découragé par les avis négatifs de son entourage. Leurs mots résonnent encore dans son esprit, semant le doute et sapant sa confiance en lui. Il se rappelle alors avoir refusé de prendre le risque de se confronter plus longtemps au regard critique de ses pairs et de sa famille.
      Marc réalise qu’il a longtemps cru que s’il s’autorisait à être pleinement lui, alors il serait rejeté. Et cette peur d’être jugé l’a retenu prisonnier d'une vie qui ne lui correspond pas vraiment. Il prend conscience que pour avancer, il doit apprendre à se libérer de l'emprise du regard des autres et à suivre sa propre voie, même si cela signifie affronter l'opposition et le scepticisme.Quelle croyance aidante incitera Marc à surmonter sa peur du jugement pour embrasser pleinement son authenticité et suivre ses aspirations les plus profondes ?`,
    response: [
      `"En étant pleinement moi-même, j'attire les bonnes personnes et les bonnes opportunités dans ma vie, créant ainsi des connexions authentiques et significatives."`,
      `"En étant pleinement moi-même, j'attire les bonnes personnes et les bonnes opportunités dans ma vie, créant ainsi des connexions authentiques et significatives."`,
      `"En étant pleinement moi-même, j'attire les bonnes personnes et les bonnes opportunités dans ma vie, créant ainsi des connexions authentiques et significatives."`,
      `"En étant pleinement moi-même, j'attire les bonnes personnes et les bonnes opportunités dans ma vie, créant ainsi des connexions authentiques et significatives."`,
    ]
  },
  {
    title: 'Chapitre 3 : Les Doutes sur la Reconversion',
    content: `Déterminé à suivre son cœur et à poursuivre sa passion pour la photographie, Marc se lance dans les démarches pour demander un congé de formation pour reconversion professionnelle. Pourtant, malgré sa détermination, des doutes sournois commencent à s'insinuer dans son esprit.
      Alors qu'il remplit le formulaire de demande, Marc sent une boule d'angoisse se former dans son estomac. Des pensées d’incertitude tourbillonnent dans sa tête : Gagner sa vie grâce à sa passion? Impossible, on ne peut pas prendre de plaisir au travail !
      Ces doutes, comme des ombres furtives, menacent de saboter ses efforts et de le maintenir prisonnier de sa zone de confort. Marc se rend compte que cette conviction est en fait une croyance limitante profondément ancrée : il se fait la promesse de noter tout ça ce soir sur son carnet.
      Quelle croyance aidante pour que Marc surmonte ses doutes et ses peurs afin d’ embrasser pleinement sa reconversion et saisir l'opportunité qui s'offre à lui ?`,
    response: [
      `“Beaucoup de personnes vivent de leur passion honnêtement, et moi aussi j'y ai droit”`,
      `“Beaucoup de personnes vivent de leur passion honnêtement, et moi aussi j'y ai droit”`,
      `“Beaucoup de personnes vivent de leur passion honnêtement, et moi aussi j'y ai droit”`,
      `“Beaucoup de personnes vivent de leur passion honnêtement, et moi aussi j'y ai droit”`,
    ]
  },
  {
    title: 'Chapitre 4 : Les Pressions Familiales',
    content: `
      Alors que Marc s'engage sur le chemin de la reconversion professionnelle, il se retrouve confronté aux mêmes réactions que chaque fois dans sa vie où il avait abordé le sujet.Les pressions et les attentes de sa famille, lorsqu'il partage son projet avec ses proches mettent en doute ses convictions. Il est accueilli par un mélange de réactions : l'encouragement chaleureux de certains sur lesquels il s’appuit, mais aussi le scepticisme et la préoccupation de d'autres.
      Les membres de sa famille expriment leurs inquiétudes quant à la stabilité financière et à la sécurité de son choix. Ils soulignent les risques inhérents à la poursuite d'une carrière artistique et les défis potentiels auxquels Marc pourrait être confronté. Leurs paroles résonnent dans son esprit, semant le doute et remettant en question sa décision.
      Marc se retrouve tiraillé entre son désir ardent de suivre sa passion et l’ importance de répondre aux attentes de sa famille. Il se sent submergé par un sentiment de responsabilité envers eux, mais aussi par le besoin de se réaliser pleinement dans sa vie professionnelle.
      Quelle croyance aidante peut permettre à Marc de trouver l'équilibre entre ses propres aspirations et les attentes de sa famille, tout en restant fidèle à lui-même et à ses rêves les plus profonds ?`,
    response: [
      `“Je peux respecter et honorer les membres de ma famille tout en restant fidèle à moi-même et en suivant mes propres désirs et aspirations.”`,
      `“Je peux respecter et honorer les membres de ma famille tout en restant fidèle à moi-même et en suivant mes propres désirs et aspirations.”`,
      `“Je peux respecter et honorer les membres de ma famille tout en restant fidèle à moi-même et en suivant mes propres désirs et aspirations.”`,
      `“Je peux respecter et honorer les membres de ma famille tout en restant fidèle à moi-même et en suivant mes propres désirs et aspirations.”`,
    ]
  }, 
  {
    title: 'Chapitre 5 : Les Aspirations Amoureuses',
    content: `Les mois ont passé. Alors que Marc trouve son équilibre professionnel et familial, il ne peut s'empêcher de ressentir un vide dans sa vie affective. Malgré son succès et son épanouissement dans d'autres domaines, il se rend compte qu'il aspire à partager sa vie avec quelqu'un de spécial.
      Les années de dévouement à sa carrière l'ont souvent éloigné des relations amoureuses sérieuses. Maintenant, face à ce nouveau chapitre de sa vie, Marc se trouve confronté à ses propres peurs et incertitudes en matière d'amour.
      Il reprend l’ écriture dans son carnet et des questions surgissent dans son esprit.
      Il se rend compte , avec tristesse, que toute ses années il s’est auto-saboté au niveau sentimental. Sa conviction de ne pas être assez bien pour être aimé l’a condamné a ecourter chaque relation sérieuse, persuadé que l’autre finirait par découvrir qu’il était indigne d’amour et l’aurait rejeté. Mieux valait quitter qu’être quitté.
      Malgré ses doutes, Marc reste optimiste quant aux possibilités qui s'offrent à lui. Il a réalisé désormais qu’il était capable de modifier sa façon de voir la vie. Il sait que l'amour véritable est un voyage qui demande du temps, de la patience et de la vulnérabilité. Il est prêt à explorer ce nouveau territoire de son être avec ouverture et courage.
      Avec quelle croyance aidante Marc arrivera-t-il à s’ ouvrir à l’amour?`,
      response: [
        `“Je mérite d'être aimé et accepté pour qui je suis, avec toutes mes qualités et mes imperfections.“`,
        `“Je mérite d'être aimé et accepté pour qui je suis, avec toutes mes qualités et mes imperfections.“`,
        `“Je mérite d'être aimé et accepté pour qui je suis, avec toutes mes qualités et mes imperfections.“`,
        `“Je mérite d'être aimé et accepté pour qui je suis, avec toutes mes qualités et mes imperfections.“`,
      ]
    },
    {
      title: 'Merci de votre participation',
      content: `Voici une description de votre résultat`,
      response: [
        `“Recomencer le test”`,
        `Retourner au menu`,
      ]
    }, 
  ]
)
const sliceOfProgressInit = ref<number>(100 / contentStory.value.length)
let newPercentage = ref<number>(sliceOfProgressInit.value)
const percentageOfProgress = ref<string>('')

onMounted(() => {
  localStorage.removeItem('testResults');
});

onUpdated(() => {
  window.scrollTo(0,0)
})

const scrollToTop = () => {
  window.scrollTo(0,0)
}

const showNextContent = (index: number): void => {
  if(currentIndex.value === contentStory.value.length - 1) {
    if(index === 0) currentIndex.value = 1
    else currentIndex.value = 0
    localStorage.clear()
    newPercentage.value = index === 0 ? sliceOfProgressInit.value * 2 : sliceOfProgressInit.value
    percentageOfProgress.value = `${Math.round(newPercentage.value)}%`
    return
  }

  if (currentIndex.value < contentStory.value.length - 1) {
    percentageOfProgress.value = `${Math.round(newPercentage.value += sliceOfProgressInit.value)}%`
    currentIndex.value++;
    getResult()
  }

  setResult(currentIndex.value, index)
};

const showPreviousContent = () => {
  percentageOfProgress.value = `${Math.round(newPercentage.value -= sliceOfProgressInit.value)}%`
  currentIndex.value--
}

const setResult = (IndexQuestion: number, indexResponse: number) => {
  const results = JSON.parse(localStorage.getItem('testResults') || '[]');
  results.push({ question: IndexQuestion, response: indexResponse });
  localStorage.setItem('testResults', JSON.stringify(results));
}

const getResult = () => {
  const savedResults = JSON.parse(localStorage.getItem('testResults') || '[]');
  results.value = savedResults.map((result: { question: number, response: number }) => {
    const question = contentStory.value[result.question]
    const response = question.response && question.response[result.response]
    return {
      question: question ? question.title : "Question non trouvée",
      response: response !== undefined ? response : "Réponse non trouvée"
    }
  })
  console.log(results.value)
}




</script>

<style>
main {
  height: 80vh;
  margin: 20px 0;
}

.fade-enter-active {
  transition: opacity 5s;
}

.content {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.btn-container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 10px;
  width: fit-content;
  margin: 20px auto;
  grid-template-areas: 
    "button_1 button_2"
    "button_3 button_4";
}

.btn-response-1{
  grid-area: button_1;
}
.btn-response-2{
  grid-area: button_2;
}
.btn-response-3{
  grid-area: button_3;
}
.btn-response-4{
  grid-area: button_4;
}

.btn{
  max-width: 350px;
  padding: 5px 10px;
  border-radius: 5px; 
  background-color: var(--vt-c-indigo);
  color: black;
  background-color:  hsla(160, 100%, 37%, 1);
  box-shadow: 5px 5px 10px rgba(0, 65, 43, 0.49);
  transition: .2s;
  cursor: pointer;
}
.btn:hover {
  font-weight: 600;
  transform: scale(1.02);
}

.btn-back {
  text-align: left;
  cursor: pointer;
}

.progress-bar-container {
  position: relative;
  width: 100%; 
  height: 15px;
  background-color: #fff
}

.progress-bar {
  height: 15px; 
  color: #000;
  border: 1px solid #fff; 
  background-color: hsla(160, 100%, 37%, 1);
}

.percentage {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: block;
}

@media screen and (max-width: 600px) {
  .btn-container {
    display: flex;
    flex-direction: column;
  }
  
}
</style>