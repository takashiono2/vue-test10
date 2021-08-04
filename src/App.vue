<template><!---->
  <v-app>
    <v-navigation-drawer app v-model="drawer" clipped>
    <!--v-navigation-drawerは、「v-app-bar」の上に追加-->
    <!--clippedは「」にナビゲーションメニューを配置させる設定。-->
    <!--propsのvalueが表示非表示するため。@clickしただけでは非表示にならないので、「」を設定し、初期値がnullの場合、非表示となる。-->
      <v-container>
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title class="title grey--text text--darken-2"><!--text-darken-2は「」を変更できる。-->
              Navigation Lists
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-divider></v-divider>
        <v-list nav dense ><!--denseを設定すると、リストの「スタイリングを調整」-->
            <v-list-group 
              v-for="nav_list in nav_lists" 
              :key="nav_list.name" 
              :prepend-icon="nav_list.icon" 
              no-action 
              :append-icon="nav_list.lists ? undefined : ''">
              <!--no-actionがないと「」の「」が設定されない、:append-iconを設定しなければ「」-->
                <template v-slot:activator>
                  <v-list-item-content>
                   <v-list-item-title>{{ nav_list.name }}</v-list-item-title>
                  </v-list-item-content>
                </template>
              <v-list-item v-for="list in nav_list.lists" :key="list.name" :to="list.link">  
                <v-list-item-content>
                  <v-list-item-title>{{ list }}</v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-list-group>
        </v-list>
      </v-container>      
    </v-navigation-drawer>
    <v-app-bar color="primary" dark app clipped-left>
      <!-- appを設定すると、「」を自動調整してくれる。「clipped-left」で通常時、ナビゲーションメニューが下、左寄せ配置になる-->
      <v-app-bar-nav-icon @click="drawer=!drawer"></v-app-bar-nav-icon>
          <!--v-app-bar-nav-iconは、「」のアイコンの事、クリック操作のため@clickを設定.-->
      <v-toolbar-title>Vuetify</v-toolbar-title>
      <v-spacer></v-spacer><!--「v-spacer」は、2つのコンポーネントの間にスペースをとれる。-->
      <v-toolbar-items><!--ボタンに「」した際に、v-app-barコンポーネントの「」分のクリック領域を持たせれる。-->
        <v-btn text to="/enterprise">For Enterprise</v-btn><!--textでボタンを「」にできる。リンク設定は、v-buttonタグに「」を加えることで設定できる。routesのpathを参照-->
          <v-menu offset-y><!--v-menuで「」できる-->
            <template v-slot:activator="{on}">
              <v-btn v-on="on" text>Support<v-icon>mdi-menu-down</v-icon></v-btn>
              <!--アイコンの設定は「」の中に「mdi-“アイコン名”」で行う。-->
            </template>
            <v-list>
            <v-subheader>Get help</v-subheader><!--v-subheaderで、「サブヘッダー」が作れる-->
                <v-list-item v-for="support in supports" :key="support.name" :to="support.link">
                  <v-list-item-icon>
                    <v-icon>{{ support.icon }}</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <v-list-item-title>{{ support.name }}</v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
            </v-list>
          </v-menu>
      </v-toolbar-items>
    </v-app-bar>
    <v-main>
      <router-view /><!--「Vue Router」がインストールされているので、「v-main」の中に「router-view」タグを挿入。-->
    </v-main>
    <v-footer color="primary" dark app>
      Vuetify
    </v-footer>
  </v-app>

</template>

<script>

export default {
  data(){
    return{
        drawer: null,
        supports:[
          {
            name: 'Consulting and suppourt',
            icon: 'mdi-vuetify',
            link: '/consulting-and-support'
          },
          {
            name: 'Discord community',
            icon: 'mdi-discord',
            link:'/discord-community'},
          {
            name: 'Report a bug',
            icon: 'mdi-bug',
            link:'/report-a-bug'
          },
          {
            name: 'Github issue board',
            icon: 'mdi-github-face',
            link:'/guthub-issue-board'
          },
          {
            name: 'Stack overview',
            icon: 'mdi-stack-overflow',
            link:'/stack-overview'
          }
        ],
        nav_lists:[
          {
            name: 'home',
            icon: 'mdi-home',
            link: '/'
          },
          {
            name: 'TodoList',
            icon: 'mdi-format-list-checks'
          },
          {
            name: 'about',
            icon: 'mdi-information-outline',
            link: '/about'
          },
          {
            name: 'Styles & animations',
            icon: 'mdi-palette',
            lists:['Colors','Content','Display']
          }
        ]
    }
  }
};
</script>
