---
title: 'Building Event System in Unity3D'
date: 2018-06-29
permalink: /posts/2018/06/unity3d-event/
tags:
  - English
  - C#
  - Unity 3D
  - Design Pattern
---

When I was developing a simple 3D game using Unity 3D, I found it non-trivial to build an event system that could handle dynamic game events efficiently and elegantly. 

## 1. Prerequisites

### 1.1 Observer Pattern

According to Wikipedia, the **observer pattern** is a [software design pattern](https://en.wikipedia.org/wiki/Design_pattern_(computer_science)) in which an [object](https://en.wikipedia.org/wiki/Object_(computer_science)#Objects_in_object-oriented_programming), called the **subject**, maintains a list of its dependents, called **observers**, and notifies them automatically of any state changes, usually by calling one of their [methods](https://en.wikipedia.org/wiki/Method_(computer_science)). (I omitted the definition in the Gang of Four book since it's not easy to understand)

Observer Pattern is often used in game when you need to build a event system. A event system is capable of notifying other classes about some specific events (player died, boss slaughtered, key item found, ...). 

### 1.2 Observer Pattern in C# Language

Observer pattern is so commonly used that C# supports observer pattern at language level, which saves us a lot of labor and potential trouble in implementing it. 

#### 1.2.1 The `delegate` keyword

`delegate` is a special data type in C# representing functions. It's similar to function pointer in C, but has the advantage of **multicasting**, which allows combining different functions into a single variable.

``` c#
delegate void MyDelegate(int num);
public void UseDelegate() {
    MyDelegate myDelegate = f;
    myDelegate += g;
    myDelegate();
}
public void f(int a) {...}
public void g(int b) {...}
```

#### 1.2.2 The `event` keyword 

The `event` data type is just similar to the `delegate` data type, but it doesn't allow any modification other than adding and removing observers to/from the `event` variable. 

```C#
public delegate void ClickAction();
public static event ClickAction OnClicked;
OnClicked += button1.ProcessClicked;
OnClicked += scene.ProcessClicked;
OnClicked -= button1.ProcessClicked;
OnClicked -= scene.ProcessClicked;
```

An important thing to notice is that a function MUST be removed from the event variable if the object it belongs to has been disabled or garbage collected, otherwise erroneous behaviors may occur.

## 2. Example Usage

Suppose we have a boss in game that we can slaughter it to win the level. When the boss died three class need to response to it. The player should cheer, the UI should display message and the game should end a few seconds later. Then we can arrange our code as follows:

``` C#
public class GameManager : MonoBehaviour {
	// Manage Events
	public delegate void BossSlaughteredAction();
	public static event BossSlaughteredAction bossSlaugheredAction;
	public static void OnBossSlaughtered() {
		if (bossSlaugheredAction != null) bossSlaugheredAction();
	}
	void OnEnable() {
		bossSlaugheredAction += HandleBossSlaughtered;
	}
	void OnDisable() {
		bossSlaugheredAction -= HandleBossSlaughtered;
	}
	public void HandleBossSlaughtered() {
		//Debug.Log("Boss Slaughtered!");
		DisplayTextAtScreen("猎得传奇猎物，游戏结束！", 5.0f);
		Invoke("ProcessGameEnding", 5.0f);
	}
    void ProcessGameEnding() {
		UnityEngine.SceneManagement.SceneManager.LoadScene("StartMenu");
	}
}
```

```C#
public class BeerAttributes : MonoBehaviour {
	[SerializeField] float health = 100.0f;
	void TakeDamage(float amount) {
		health -= amount;
		if (health <= 0) {
			this.enabled = false;
			//Debug.Log("Die");
			GameManager.OnBossSlaughtered();
		}
	}
}
```

``` c#
public class WolfEventHandler : MonoBehaviour {
	void OnEnable() {
		GameManager.bossSlaugheredAction += HandleBossSlaughtered;
	}
	void OnDisable() {
		GameManager.bossSlaugheredAction -= HandleBossSlaughtered;
	}
	void HandleBossSlaughtered() {
		Animator animator = GetComponent<Animator>();
		animator.SetTrigger("Cheer");
	}
}
```