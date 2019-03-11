## auto占位符
### 历史与发展
	在c++11前，auto拥有“存储期指定符”的语义，标识临时变量。c++11起废弃了这个用法，引入了新的用法。
### auto的用处
	C++11中引入的新auto主要有两种用途，即自动类型推断和返回值占位。
	类型推断：对于变量，指定要从其初始化器自动推导出其类型。对于非类型模板形参，指定要从参数推导出其类型。(C++17 起)
	返回值占位：对于函数，指定其返回类型从其 return 语句推导出。(C++14 起)
	显而易见地，使用auto可以加快c++编程的效率，并且在某些地方使代码很大程度地简洁。
### 一些注意
	可以使用valatile，pointer（*），reference（&），rvalue reference（&&） 来修饰auto；
	用auto声明的变量必须初始化；
	auto会退化成指向数组的指针，除非被声明为引用。
### 一个实际使用的例子
	...
	pParam->paramList.clear();
	for (const auto& rMoveAct : pMoveAc->GetMoveCardActList())
	{
		if (rMoveAct.mode != CMoveCardAction::Mode_Judge_DisCard || rMoveAct.allPlayCardList.empty() ||
			NULL == rMoveAct.pToZone || rMoveAct.pToZone->GetZoneType() != pGame->GetDiscardZone().GetZoneType())
			continue;
		for (auto &pCard : rMoveAct.allPlayCardList)
		{
			if (pCard != NULL)
				pParam->paramList.push_back(pCard->GetCardId());
		}
	}

	事实上函数GetMoveCardActList()的返回值类型为:
	typedef std::list<TMoveCardsAct> MoveCardActList
	在这里auto拯救了我们的代码。