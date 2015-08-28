using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using LeagueSharp;
using System.Drawing;
using LeagueSharp.Common;

namespace Monster_Vayne
{
    class Program
    {
        private static String ChampionName = "Vayne";
        public static Obj_AI_Hero Player;
        private static Menu _menu;
        private static Orbwalking.Orbwalker _orbwalker;
        private static Spell Q, W, E, R;
     

        static void Main(string[] args)

        {
             CustomEvents.Game.OnGameLoad += Game_OnGameLoad;
             Game.PrintChat("Credit : ErcaN");
           
        }
        private static void Game_OnGameLoad(EventArgs args)
        {
            Player = ObjectManager.Player;
            if (Player.ChampionName != ChampionName)
            {
                return;
            }
            _menu = new Menu("Monster Vayne", "monster.vayne", true);
            var orbwalker = new Menu("Orbwalker", "monter.vayne.orbwalker");
            _orbwalker = new Orbwalking.Orbwalker(orbwalker);

            _menu.AddSubMenu(orbwalker);

            var targetSelectorMenu = new Menu("Target Selector", "Target Selector");
            TargetSelector.AddToMenu(targetSelectorMenu);
            _menu.AddSubMenu(targetSelectorMenu);

            var ComboMenu = new Menu("Combo", "monster.vayne.combo");
            {
                ComboMenu.AddItem(new MenuItem("monster.vayne.kullanq", "Use Q").SetValue(true));
                ComboMenu.AddItem(new MenuItem("monster.vayne.kullanw", "Use W").SetValue(true));
                ComboMenu.AddItem(new MenuItem("monster.vayne.kullane", "Use E").SetValue(true));
                ComboMenu.AddItem(new MenuItem("monster.vayne.kullanr", "Use R").SetValue(true));
            }
            _menu.AddSubMenu(ComboMenu);

        

          

            //var HarrasMenu = new Menu("Harras", "monster.vayne.harras");
            //{
            //    ComboMenu.AddItem(new MenuItem("monster.vayne.harraslaq", "Use Q").SetValue(true));
            //    ComboMenu.AddItem(new MenuItem("monster.vayne.harraslaw", "Use W").SetValue(true));
            //    ComboMenu.AddItem(new MenuItem("monster.vayne.harraslae", "Use E").SetValue(true));
            //    ComboMenu.AddItem(new MenuItem("monster.vayne.harraslar", "Use R").SetValue(true));


            //}
            //_menu.AddSubMenu(HarrasMenu);
        
           _menu.AddToMainMenu();

          

        }
       
    }
}
