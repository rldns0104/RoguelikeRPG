# RoguelikeRPG
### Add
- Source.c -> main function
    line16 
  
        _showInventory(hCSB, pRL->pPC);
        _showPlayerInfo(hCSB, pRL->pPC);
        _showScore(hCSB, pRL);
        
- roguelike_ui.c
    line739  
  
       void _showInventory(HANDLE hCSB, PENT pPC)
      {
	      SHORT xt = UI_BASIC_WIDTH;
	      SHORT yt = INVENTORY_UI_BASIC_HEIGHT;
	      SetConsoleTextAttribute(hCSB, _FW);
	      _setCursorPos(hCSB, xt, yt);
	      printf("=======Inventory======");
        
          SHORT invenNum = 1;
	      for (int i = 0; i < 2; i++)
	      {
		      for (int j = 0; j < 5; j++)
      	{
      		_setCursorPos(hCSB, xt, yt + (j * 2 + 2));
      		printf("%d.", invenNum);
      
      		if (pPC->items[invenNum]->pItem != NULL)
      		{
      			printf("%s", pPC->items[invenNum]->pItem->name);
      			printf("(%d)", pPC->items[invenNum]->num);
      		}
      		invenNum++;
      		if (invenNum == 10)
      			break;
      	}
		     xt += 12;
          }
	     _setCursorPos(hCSB, 0, 0);
       }
      void _showPlayerInfo(HANDLE hCSB, PENT pPC)
      {
	      SHORT xt = UI_BASIC_WIDTH;
	      SHORT yt = STAT_UI_BASIC_HEIGHT;
	      SetConsoleTextAttribute(hCSB, _FW);
	      _setCursorPos(hCSB, xt, yt);
	      printf("======PlayerInfo======");
      
	      for (int i = 0; i < NUM_STATS; i++)
	      {
		      _setCursorPos(hCSB, xt, yt + (i * 2 + 2));
		      switch (i)
		      {
		      case 0:
			      printf("LV.%d", pPC->stats[_LV]);
			      break;
		      case 1:
			      printf("HP = %d/%d", pPC->stats[_curHP], pPC->stats[_maxHP]);
			      break;
		      case 2:
			      printf("ATK = %d (+%d)", pPC->stats[_ATK] - pPC->stats[_tmpATK], pPC->stats[_tmpATK]);
			      break;
		      case 3:
			      printf("DEF = %d (+%d)", pPC->stats[_DEF] - pPC->stats[_tmpDEF], pPC->stats[_tmpDEF]);
			      break;
		      case 4:
			      printf("EXP = %d/%d", pPC->stats[_curEXP], pPC->stats[_maxEXP]);
			      break;
		      case 5:
			      printf("WON = %d", pPC->stats[_WON]);
			      break;
		      }
	      }
	      _setCursorPos(hCSB, 0, 0);
      }
      
      void _showScore(HANDLE hCSB, PRL pRL)
      {
	      SetConsoleTextAttribute(hCSB, _FW);
	      SHORT xt = UI_BASIC_WIDTH;
	      SHORT yt = 1;
      
	      _setCursorPos(hCSB, xt, yt);
	      printf("Score = %d ST = %d", pRL->pPC->stats[_SCORE], pRL->curIdx + 1); //점수가 999,999를 넘을 때 글씨가 UI를 뚫는 것을 미연에 방지
      
	      _setCursorPos(hCSB, 0, 0);
       }
       

### Provide
- let player to know current PlayerInfo(score, stats, inventory, etc.)
