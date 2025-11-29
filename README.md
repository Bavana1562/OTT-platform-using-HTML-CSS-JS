# OTT-platform-using-HTML-CSS-JS

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>OTT Platform UI</title>
</head>
<body>
  <header>
    <div class="nav container">
      <div class="left">
        <div class="logo">OTT STREAMING</div>
      </div>
      <div class="menu">
        <a href="#">Home</a>
        <a href="#">TV Shows</a>
        <a href="#">Movies</a>
        <a href="#">My List</a>
        <a href="#">My Favourite</a>
      </div>
      <div class="nav-right">
        <input id="searchInput" class="search" placeholder="Search movies">
        <div class="avatar" title="Profile"></div>
      </div>
    </div>
  </header>
  <section id="banner" class="banner">
    <div class="banner-content container">
      <h1 id="bannerTitle">Hidden Love</h1>
      <p id="bannerOverview">Since high school, Sang Zhi has had a crush on Duan Jiaxu. When fate brings them together again, they find a chance to embark on a sweet relationship.</p>
      <button class="btn play" id="bannerPlay">Play</button>
      <button class="btn info" id="bannerInfo">More Info</button>
    </div>
  </section>
  <main>
    <div class="container" id="rowsRoot"></div>
  </main>
  <div id="modal" class="modal" aria-hidden="true">
    <div class="modal-card">
      <div id="modalHero" class="modal-hero"></div>
      <div class="modal-body">
        <h2 id="modalTitle"></h2>
        <p id="modalDesc" class="muted"></p>
        <p><strong>Genre:</strong> <span id="modalGenre"></span></p>
        <p><strong>Year:</strong> <span id="modalYear"></span></p>
        <button id="addWatchlist" class="watchlist-btn">Add to Watchlist</button>
        <button id="closeModal" class="watchlist-btn close-btn">Close</button>
      </div>
    </div>
  </div> 
</body>
</html>
<style>
   :root{
  --bg:#121212;
  --card:#1f1f1f;
  --muted:#ddd;
  --accent:#e50914;
  --glass: rgba(255,255,255,0.05);
  --max-width:1200px;
  --gap:8px;   
}
*{box-sizing:border-box;}
body{
  margin:0;
  font-family: 'Times New Roman', Times, serif;
  background-color: var(--bg);
  color:#fff;
}
.container{
  max-width: var(--max-width);
  margin:0 auto;
  padding:24px;
}
header{
  position:sticky; top:0; z-index:40;
  background:linear-gradient(180deg,rgba(0,0,0,0.85),transparent);
  backdrop-filter:blur(6px);
}
.nav{
  display:flex;
  justify-content:space-between;
  align-items:center;
  padding:12px 24px
}
.logo{
  font-weight:800;
  color:var(--accent);
  letter-spacing:2px;
  font-size:20px;
}
.menu{
  display:flex;
  gap:18px;
}
.menu a{
  color:#ddd;
  text-decoration:none;
  font-size:14px;
}
.nav-right{
  display:flex;
  align-items:center;
  gap:10px;
}
.search{
  background:var(--glass);
  border:none;
  padding:8px 12px;
  border-radius:6px;
  color:#fff;
}
.avatar{
  width:34px;
  height:34px;
  background:linear-gradient(45deg,#666,#444);
  border-radius:4px;
}
.banner{
  position:relative;
  height:58vh;
  background-size:cover;
  background-position:center;
  display:flex;
  align-items:flex-end;
  padding-bottom:50px;
}
.banner::after{
  content:"";
  position:absolute;top:0;left:0;right:0;height:100%;
  background:linear-gradient(180deg,rgba(0,0,0,0.5),rgba(0,0,0,0.9));
}
.banner-content{
  position:relative;
  z-index:2;
  padding:0 24px;
  max-width:60%;
}
.banner h1{
  margin:0;
  font-size:clamp(24px,4vw,40px);
}
.banner p{
  color:#ccc;
  line-height:1.4;
  margin-top:10px;
}
.btn{
  padding:10px 16px;
  border:none;
  border-radius:6px;
  margin-top:12px;
  font-weight:600;
  cursor:pointer;
}
.btn.play{background:var(--accent);color:#fff;}
.btn.info{background:rgba(255,255,255,0.1);color:#fff;margin-left:8px;}
.section{
  padding:12px 0;
}
.section h2{
  margin:0 0 10px 0;
  font-size:18px;
}
.row{
  position:relative;
}
.row-track{
  display:flex;
  gap:var(--gap);
  overflow-x:auto;
  scroll-behavior:smooth;
  padding-bottom:6px;
}
.row-track::-webkit-scrollbar{
  height:6px;
}
.row-track::-webkit-scrollbar-thumb{
  background:rgba(255,255,255,0.1);
  border-radius:10px;
}
.card{
  min-width:150px;
  flex:0 0 auto;
  background: var(--card);
  border-radius:6px;
  overflow:hidden;
  cursor:pointer;
  transition: transform .25s ease;
}
.card img{
  width:100%;        
  height:170px;      
  object-fit:cover;  
  display:block;
  border-radius:6px;
}
.card:hover{
  transform:scale(1.05);
}
.card .meta{
  padding:8px;
  font-size:10px;
  color:#ccc;
}
.arrow{
  position:absolute;
  top:40%;
  transform:translateY(-50%);
  background:rgba(0,0,0,0.6);
  border:none;
  color:#fff;
  border-radius:30%;
  width:28px;
  height:28px;
  cursor:pointer;
  display:flex;
  align-items:center;
  justify-content:center;
}
.arrow.left{left:4px;}
.arrow.right{right:4px;}
.modal{
  position:fixed;
  inset:0;
  display:none;
  align-items:center;
  justify-content:center;
  background:rgba(0,0,0,0.6);
  z-index:80;
}
.modal.open{
  display:flex;
}
.modal-card{
  background:var(--card);
  max-width:840px;
  width:95%;
  border-radius:10px;
  overflow:hidden;
  display:grid;
  grid-template-columns:1fr 320px;
}
.modal-hero{
  height:250px;  
  background-size:cover;
  background-position:center;
  padding:20px;
}
.modal-body{
  padding:18px;
  color:#fff;
}
.watchlist-btn{
  padding:8px 12px;
  border-radius:6px;
  border:none;
  cursor:pointer;
  margin-top:8px;
}
.close-btn{
  background:transparent;
  border:1px solid rgba(255,255,255,0.2);
  color:#fff;
  margin-left:8px;
}
.muted{color:#ccc;}
@media (max-width:900px){
  .modal-card{grid-template-columns:1fr;}
  .banner-content{max-width:90%;}
  .card{min-width:110px;}
}
@media (max-width:500px){
  .menu{display:none;}
  .banner{height:46vh;}
  .card{min-width:100px;}
}
</style>
<script>
const sampleData = {
  banner: {
    id: 1001,
    title: 'Hidden Love',
    overview: 'Since high school, Sang Zhi has had a crush on Duan Jiaxu. When fate brings them together again, they find a chance to embark on a sweet relationship.',
    image: 'https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcQmrlw8d5OrWTAzKI-pLX_pOX38knkqC651g44pYhbcZ1sIWxDD'
  },
  rows: [
    {
      id: 'trending',
      title: 'Trending Now',
      items: [
        { id: 1, title: 'Here We Meet Again', overview: 'A young businesswoman takes over her family s struggling company branch, reuniting with her former crush. Together, they navigate corporate challenges while working on Chinas GPS technology, rekindling old feelings along the way.', image: 'https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcTDBH5p8LRr1rNEm1jgX0ttV5zGmo5KYpiU2IQUlZAyCnsidweT', genre: 'TV series', year: 2023 },
        { id: 2, title: 'When the Phone Rings', overview: 'A rising politician and his nonverbal wifes tense marriage begins to unravel after a call from a kidnapper turns their lives upside down.', image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRNhkl3XwZ2j5ScgxlkX6M2rzHdJsObIVh86PpxmNkYtJAW-AUP', genre: 'TV Show', year: 2024 },
        { id: 3, title: 'Lovely Runner', overview: 'Right after top star Ryoo Seon-jae ends his life, his top fan Im Sol somehow time-travels back to when they were in high school and tries to protect him. A fantasy romance unfolds where people who missed each other in time finally meet.', image: 'https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcSXdxGXrFLMSLnStr9xzQPfuc-zSu2XJ5dP2KvYQ2Mt10O21m_I', genre: 'TV Series', year: 2024 },
        { id: 4, title: 'Only for Love', overview: 'Zheng Shu Yi is a hard-working reporter for one of China leading financial newspapers. Shi Yan, the businessman, is looking to make a series of investments. Could this blossoming working relationship also lead them on the path to love?', image: 'https://s.isanook.com/mv/0/ui/31/158551/jQl3KB_3f.jpg', genre: 'TV series', year: 2023 },
        { id: 5, title: 'My Amazing Boyfriend', overview: 'A 500-year-old mutant saves a B-actress, uncovering a centuries-old conspiracy that will transform their world forever. Read synopsis.', image: 'https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcT03I5pJwIK2-tnwA7rX0OePBJnSaQ8uBwJtRYlzK4GX6gAi5dr', genre: 'Romance', year: 2016 },
        { id: 6, title: 'F4 Thailand: Boys Over Flowers', overview: 'An ordinary, poor girl, Gorya, stands up to and through a series of mishaps and conflicts, falls in love with Thyme, the leader of the F4, the most powerful young men in Thailand.', image: 'https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcTNkjlweXNrTblTL57Aol_H0dcxE3VmQ9JtS6vivIdxC6mKVwN-', genre: 'Drama', year: 2021 },
        { id: 7, title: 'Queen of Tears', overview: 'A miraculous love story of a married couple overcoming a dizzying crisis.', image: 'https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcRuDYPchYq0UeGlpm1UkcIeSG-fyt8mjyfWDhQApjqFPIR1vzLh', genre: 'Romance', year: 2024 },
        { id: 8, title: 'Faceless Love', overview: 'Vikij is a handsome, rich and intelligent young man who suffers from prosopagnosia, that is, he cannot recognize faces. For this reason, he decides to hire Mirin, an assistant to help him relate to the rest of the world.', image: 'https://upload.wikimedia.org/wikipedia/en/a/ad/Faceless_Love_2023_Official_Poster.png', genre: 'Romance', year: 2023 },
    ]
    },
    {
      id: 'drama',
      title: 'Drama Series',
      items: [
        { id: 11, title: 'Doom at Your Service', overview: 'Park Bo Young curses her life and luck, summoning Doom messenger Seo In Guk who gives her only 100 days to live in the romantic comedy "Doom at Your Service."', image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQeH9JlcJOGntB5YGKdzxd-qsSdVH4P6iIbgVeRTVMlY-L3wJ_1', genre: 'Drama', year: 2021 },
        { id: 12, title: 'Outlander', overview: 'A nurse in World War II mysteriously goes back in time to Scotland in 1743. There, she meets a dashing Highland warrior and gets drawn into an epic rebellion.', image: 'https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcSkTtM0gf2V39uLRwqZQPlBZRf4qp2ftPyY4FlmT1BWw46iw2SA', genre: 'Drama', year: 2014 },
        { id: 13, title: 'Stranger Things', overview: 'In 1980s Indiana, a group of young friends witness supernatural forces and secret government exploits. As they search for answers, the children unravel a series of extraordinary mysteries.', image: 'https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcQaZ3jDdik4aF0G_eU607vjeBsMzReqr8E8riWMU87ZocGDsfPq', genre: 'Drama', year: 2016 },
        { id: 14, title: 'Emily in Paris', overview: 'A young American woman from the Midwest is hired by a marketing firm in Paris to provide them with an American perspective on things.', image: 'https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcRSd6R59-rwEgp8w0fOWYj_U0yTVyxjOcfKOWILcvmRgedSuuo6', genre: 'Drama', year: 2020 },
        { id: 15, title: 'My Dearest Nemesis', overview: 'An ambitious planner gets off to a rocky start with her new boss, but hes got a secret: hes her childhood gaming crush! Read synopsis.', image: 'https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcTi3-RCPBPLyewEkdz-WASeuOeS67RZM9vmu3ggfJGE8vWhhg4b', genre: 'Rom-com', year: 2025 },
        { id: 16, title: 'Its Okay to Not Be Okay', overview: 'An extraordinary road to emotional healing opens up for an antisocial childrens book writer and a selfless psych ward caretaker when they cross paths.', image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR5xje5GGu_-6y_2zzlC5g93ghc8l7ORBAIn4Ve0p30O7xGJ3p_', genre: 'Drama', year: 2020 },
        { id: 17, title: 'Good Boy', overview: 'A loyal dog moves to a rural family home with his owner, only to discover supernatural forces lurking in the shadows. As dark entities threaten his human companion, the brave pup must fight to protect the one he loves most.', image: 'https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcSCXcZFwdIRAKiHT2hzWX3VDmtU9nXVBB3Zo1-D1N51Z6l5GVrg', genre: 'Drama', year: 2025 },
        { id: 18, title: 'The Girlfriend', overview: 'The Girlfriend is a psychological thriller television miniseries for Amazon Prime Video directed by Robin Wright and Andrea Harkin.', image: 'https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcQSDKJJbrAlhez-_qFHsNabgqhmMcBd1FBxhBv3FMIh-kma8F8y', genre: 'Drama', year: 2025 }
      ]
    },
    {
      id: 'action',
      title: 'Action Movies',
      items: [
        { id: 21, title: 'Pushpa 1: The Rise', overview: 'The film follows Pushpa, a daily wage labourer who rises through the ranks of a syndicate involved in smuggling red sandalwood.', image: 'https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcTEBj8p-ynRkaIk4luHnF02ahyCJ6epbBOt_6dTS5fBWs7rqC-E', genre: 'Action', year: 2021 },
        { id: 22, title: 'Pushpa 2: The Rule', overview: 'A smuggling kingpin faces off against a vengeful rival while manipulating politics, making big deals, and navigating tense confrontations.', image: 'https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcTK_Cq35EB_KZmwZ-8M--dRvv-e6WPhQlaNFnoMXKXivM6AihMq', genre: 'Action', year: 2024 },
        { id: 23, title: 'They Call Him OG', overview: 'After vanishing from Mumbais underworld for a decade, mob boss Ojas Gambheera resurfaces seeking vengeance against rival crime lords.', image: 'https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcQSeTZr0-b7Zg2aw_Kj4ejYMWB3HE8dl0G51HRWg3FtoDyVXZpt', genre: 'Action', year: 2025 },
        { id: 24, title: 'Salaar: Part 1 – Ceasefire', overview: 'In dystopian Khansaar, two characters navigate a complex relationship amid power struggles and shifting alliances. Their journey unfolds in a tense, futuristic world filled with conflict and drama.', image: 'https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcQtqR7E0nfNEQBDpZasJ04uz-7zpzLGYl0PDNX8oSOLitkl7tGB', genre: 'Action', year: 2023 },
        { id: 21, title: 'HIT: The First Case', overview: 'An officer of the Homicide Intervention Team who frequently suffers from having his panic attacks does everything in his power to rescue a woman who went missing.', image: 'https://upload.wikimedia.org/wikipedia/en/1/12/HIT_The_First_Case.jpg', genre: 'Action', year: 2020 },
        { id: 22, title: 'HIT: The Second Case', overview: 'A laid back cop, works in AP HIT, has to take up a gruesome murder case. As KD unravels the layers of the crime, the stakes rise unbelievably high.', image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSBOZXhSRcrZq4F9OoSe7wAbrNc1w0lyPHh4IxkhJqTpfn5_V7v', genre: 'Action', year: 2022 },
        { id: 23, title: 'HIT: The Third Case', overview: 'The Homicide Intervention Team (HIT) sends ruthless police officer Arjun Sarkaar to find a group of killers and stop their grisly murder spree.', image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSK1WZJzWfv3XRZcpZN5tFPrMBnbjY7W0F30Vjd_HNFk2xKjdLxB3KENmGhkWde9gdchQLBdw&s=10', genre: 'Action', year: 2025 },
        { id: 24, title: 'V', overview: 'A celebrated cop attempts to hunt down a serial killer who has specifically challenged him to put an end to the killing spree.', image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR_dA0vsb1hrq-j1OJMPmem8qxbgL_xNZP4kECVVqCY_oIbq21ZT0fdtteIrIK5diZUF0W8Wg&s=10', genre: 'Action', year: 2020 },
    ]
    },
    {
      id: 'newreleases',
      title: 'New Releases',
      items: [
        { id: 31, title: 'The Manipulated', overview: 'The Manipulated: With Ji Chang-wook, Do Kyung-soo, Lee Kwang-soo, Jo Yoon-soo. Mild-mannered Tae Jung is wrongfully imprisoned for a heinous crime.', image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQLiUMb3BKVHilcP-8d_tXTkX7UA6Zu5SxAT_tPbl3KaVswDDTy', genre: 'Sci-Fi', year: 2025 },
        { id: 32, title: 'As You Stood By', overview: 'Two women are driven to the brink, facing an inescapable reality that forces them to consider murder as their only way out.', image: 'https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcQXT4U3JAgWjYHBxrFjumEFxYKpyjZ4jj-A2bsh91D0wEAORNUg', genre: 'Action', year: 2025 },
        { id: 33, title: 'Dear X', overview: 'An actress abused as a child will stop at nothing to get revenge on those who wronged her – can her stepbrother save her from herself? Read synopsis.', image: 'https://asianwiki.com/images/c/c3/Dear_X-p.jpg', genre: 'Thriller', year: 2025 },
        { id: 34, title: 'Call My Agent!', overview: 'At a top Paris talent firm, agents scramble to keep their star clients happy -- and their business afloat -- after an unexpected crisis.', image: 'https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcQO1WK6K2l9h8RUsjloSVto_a_JeMYHBhYXwNp6jr8YDebSQxGY', genre: 'Drama', year: 2015 },
        { id: 35, title: 'Dark', overview: 'A family saga with a supernatural twist, set in a German town where the disappearance of two young children exposes the relationships among four families.', image: 'https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcTnPXL0OklxeuT6B2J1jLwJX9Uhczxwa0SX27UiE6cj0GDFq0zO', genre: 'Mystery', year: 2017 },
        { id: 36, title: 'Love Again', overview: 'Still grieving her fiancés death, an artist texts her deepest thoughts to his phone and forms a bond with the man who receives them by chance.', image: 'https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcRE-9EWmpzlXY6RtQc3baY6Xg_vVs_7QxAa9HGfpunWUO22_tWT', genre: 'Comedy', year: 2023 },
        { id: 37, title: 'In Your Dreams', overview: 'A sister and brother journey into the wildly absurd landscape of their own dreams to ask the wish-granting Sandman for the perfect family.', image: 'https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcT3F_-uWk2cvCARM0mQpiiO03rcdZ8c_UhOzdzasvzbyoyLGHQD', genre: 'Comedy', year: 2025 },
        { id: 38, title: 'Jingle Bell Heist', overview: 'Two down-on-their-luck hourly workers team up to rob a posh London department store on Christmas Eve. Will they steal each others hearts along the way?', image: 'https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcQy5mByP_qWuud9VUkczd6Hp78b6pOTBuXAvp3ywtOT8gZMqek_', genre: 'Comedy/Romance', year: 2025 },
      ]
    },
    {
      id: 'popular',
      title: 'Popular on Streamy',
      items: [
        { id: 41, title: '20th Century Girl', overview: 'In 1999, a teen with a heart of gold begins keeping close tabs on a popular classmate as a favor to her smitten best friend.', image: 'https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcSCIx0KkosDF9n5wcKdM74toUWM6yDk-WErjLm9isaYOjpZtP_N', genre: 'Comedy', year: 2022 },
        { id: 42, title: 'Tune in for Love', overview: 'In 1994 during the IMF crisis, two people meet while exchanging stories on a radio program. They fall in love, but cant quite seem to get the timing right.', image: 'https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcQbcrqAcSiPUY3pO-TtS9iOvAZqdrAy55ipgNgBf9ptqR1JPKrn', genre: 'Comedy', year: 2019 },
        { id: 43, title: 'Ditto', overview: 'Yong hears a strangers voice from the future, connecting them to each other and sharing their love stories.', image: 'https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcTmJZZeleWPuseU8vktzuOdEFErrpMpeoLlKaZMYkq25uqQk6yn', genre: 'Sci-fi', year: 2022 },
        { id: 44, title: 'The Snowman', overview: 'The Snowman is a 2017 psychological thriller film directed by Tomas Alfredson and written by Peter Straughan, Hossein Amini, and Søren Sveistrup.', image: 'https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcQYFsy2gEQ3AREWj6aLN8E_Q3HQ0__iGIeC6ty6cQgvftWh_xg5', genre: 'Thriller', year: 2017 },
        { id: 45, title: 'Train Dreams', overview: 'A logger leads a life of quiet grace as he experiences love and loss during an era of monumental change in early 20th-century America.', image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTY1BYGgp0XNG58y7XyXGHrUf_PM-vfx85maGj-yi5AqlXyuQ8z', genre: 'Drama', year: 2025 },
        { id: 46, title: 'The Running Man', overview: 'The Running Man is a 2025 dystopian action thriller film produced and directed by Edgar Wright and written by Wright and Michael Bacall.', image: 'https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcSFi22JqL8QxVTq9TKUtmTeoPvUxHE2BwlPmfZ9UOnrRq7HM218', genre: 'Sci-fi/Adventure', year: 2025 },
        { id: 47, title: 'Babygirl', overview: 'A high-powered CEO puts her career and family on the line when she begins a torrid affair with her much younger intern.', image: 'https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcT80osAslhWylp6sGe1HcFBYesGYfagrgbFdsEIreaHkYJHVMbb', genre: 'Thriller/Erotic', year: 2024 },
        { id: 48, title: 'Weapons', overview: 'Weapons blends mystery, horror, and dark humor through an innovative narrative with multiple perspectives and non-linear storytelling.', image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS9-FkFMeOIyaH7KEDXFhc3p8itdq1EZGDKYmWhwC0iry-Ka3Pr', genre: 'Horror/Mystery', year: 2025 },
      ]
    }
  ]
};
const rowsRoot = document.getElementById('rowsRoot');

function createRow(row){
  const section = document.createElement('section');
  section.className = 'section';
  const h = document.createElement('h2'); h.textContent = row.title;
  section.appendChild(h);

  const wrapper = document.createElement('div'); wrapper.className = 'row';

  const leftBtn = document.createElement('button'); leftBtn.className='arrow left'; leftBtn.innerHTML='&#10094;';
  const rightBtn = document.createElement('button'); rightBtn.className='arrow right'; rightBtn.innerHTML='&#10095;';

  const track = document.createElement('div'); track.className='row-track'; track.setAttribute('data-row-id',row.id);

  leftBtn.addEventListener('click', ()=>scrollRow(track,-400));
  rightBtn.addEventListener('click', ()=>scrollRow(track,400));

  row.items.forEach(item=>{
    const card = document.createElement('div'); card.className='card';
    card.setAttribute('data-title',item.title.toLowerCase()); card.setAttribute('data-id',item.id);
    const img = document.createElement('img'); img.src=item.image; img.alt=item.title;
    const meta = document.createElement('div'); meta.className='meta';
    meta.innerHTML = `<div style="font-weight:700">${item.title}</div><div class="muted">${item.genre} • ${item.year}</div>`;
    card.appendChild(img); card.appendChild(meta);
    card.addEventListener('click', ()=>openModal(item));
    track.appendChild(card);
  });

  wrapper.appendChild(leftBtn); wrapper.appendChild(track); wrapper.appendChild(rightBtn);
  section.appendChild(wrapper);
  return section;
}

function scrollRow(el,amount){ el.scrollBy({left:amount, behavior:'smooth'}); }

function renderAll(){
  const banner = sampleData.banner;
  document.getElementById('banner').style.backgroundImage=`url('${banner.image}')`;
  document.getElementById('bannerTitle').textContent=banner.title;
  document.getElementById('bannerOverview').textContent=banner.overview;

  sampleData.rows.forEach(r=>{
    const rowEl = createRow(r);
    rowsRoot.appendChild(rowEl);
  });
}

const modal = document.getElementById('modal');
const modalHero = document.getElementById('modalHero');
const modalTitle = document.getElementById('modalTitle');
const modalDesc = document.getElementById('modalDesc');
const modalGenre = document.getElementById('modalGenre');
const modalYear = document.getElementById('modalYear');
const addWatchlistBtn = document.getElementById('addWatchlist');
const closeModalBtn = document.getElementById('closeModal');

function openModal(item){
  modal.classList.add('open');
  modalHero.style.backgroundImage=`url('${item.image}')`;
  modalTitle.textContent=item.title;
  modalDesc.textContent=item.overview;
  modalGenre.textContent=item.genre;
  modalYear.textContent=item.year;

  const wl = getWatchlist();
  addWatchlistBtn.textContent = wl[item.id] ? 'Remove from Watchlist' : 'Add to Watchlist';
  addWatchlistBtn.onclick=()=>toggleWatchlist(item);
}

function closeModal(){ modal.classList.remove('open'); }
closeModalBtn.addEventListener('click',closeModal);
modal.addEventListener('click',(e)=>{if(e.target===modal) closeModal();});

function getWatchlist(){return JSON.parse(localStorage.getItem('streamy_watchlist')||'{}');}
function saveWatchlist(obj){localStorage.setItem('streamy_watchlist',JSON.stringify(obj));}
function toggleWatchlist(item){
  const wl=getWatchlist();
  if(wl[item.id]){ delete wl[item.id]; addWatchlistBtn.textContent='Add to Watchlist'; }
  else{ wl[item.id]=item; addWatchlistBtn.textContent='Remove from Watchlist'; }
  saveWatchlist(wl);
}

// Search functionality
const searchInput = document.getElementById('searchInput');
searchInput.addEventListener('input',(e)=>{
const q=e.target.value.trim().toLowerCase();
  const cards=document.querySelectorAll('.card');
  cards.forEach(c=>{ const title=c.getAttribute('data-title'); c.style.display=title.includes(q)?'block':'none'; });
});

// Banner buttons 
document.getElementById('bannerInfo').addEventListener('click',()=>{
  const b = sampleData.banner;
  openModal({id:b.id,title:b.title,overview:b.overview,image:b.image,genre:'Drama',year:2023});
});
document.getElementById('bannerPlay').addEventListener('click',()=>{
  alert('Play action — in a real app you would open a video player.');
});

//  Init 
renderAll();
document.addEventListener('keydown',(e)=>{if(e.key==='Escape') closeModal();});

</script>
