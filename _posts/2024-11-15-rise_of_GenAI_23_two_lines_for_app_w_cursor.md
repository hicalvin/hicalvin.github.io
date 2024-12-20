---
layout: post
title:  "生成式AI的崛起23: Cursor + Qwen Coder - 两句话生成一个 Java 运行程序"
date: 2024-11-15 13:27:50 +0800
category: tech
---

如今 Cursor 在 AI IDE 这块已经是独领风搔。它虽然是基于 VS Code， 但是从非常基本的内核就开始扩展加入 AI 模块，使的整个 Cursor 的使用体验非常流畅。 用非常简单的 command + K 和 command + L 就能轻松召唤出 AI 助手，通过 prompt 就可以直接生成想要的代码或者给出代码建议。 这种自然而然的使用方式，让使用者可以非常沉浸式的专注于自己想要完成的代码逻辑，无需在 IDE 和浏览器之间来回跳转。

Cursor 的另一个非常大的优势是，它支持非常丰富的编程语言，包括 Python、Java、C++、JavaScript、C#、Go、Rust、PHP、Ruby、Swift、Kotlin、Scala、Perl、Lua、Bash 等。所以无论你是什么技术栈工程师，都可以非常容易的享受 Cursor 提供的便利。

但 Cursor 最大的优势，是可以轻松接入不同的 LLM，例如，你可以轻松接入 OpenAI 的 GPT-4，也可以轻松接入 Anthropic 的 Claude 等。 而最近刚刚发布的免费的Qwen Coder，因为在各项编码评测中都获得高分，已经在第一时间得到了关注。 今天抽了些时间，就尝试了 Cursor + Qwen Coder，并只需要写两句话，就可以轻松生成 Java 程序。

## 配置

首先是在 Cursor 中配置好 Qwen Coder，在 Cursor 的`Setting -> Cursor Settings -> Models`中，把其他的 Models 都可以关闭，然后增加一个 Model，比如名叫 `Coder`， 然后在 `OpenAI API Key / Override OpenAI Base URL` 这里添加 `https://coder.gaia.domains/v1`, 在填 Key 那里可以随便输入字符串，比如 `GAIA` 就可以。 这样基于 Gaia 的Coder 就可以作为 LLM 使用了。

## 示例

在 IDE 种，直接通过 command + K 召唤出助手，在弹出的浮动框右下角就可以看到 `Coder` 这个模型，然后直接输入 prompt :

```shell
Code a game of playing puzzle  
```

接着 Cursor 就开始生成一些代码，其中包含了一些并未被引入的依赖包，比如 `Random`， `Scanner`， `ArrayList` 等。

于是我在全文选中的情况下，再次输入：

```shell
Please add missed library
```

Cursor 不仅给我在前面生成了确实的依赖包，而且很好的把代码进行了重新整理，让这个代码的格式更加容易阅读，最终的代码如下：

```java
package io.demo.example;

import java.util.Random;
import java.util.Scanner;

public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Welcome to the Puzzle Game!");

        // Example puzzle: A simple number guessing game
        Random random = new Random();
        int secretNumber = random.nextInt(10) + 1; // Generates a number between 1 and 10
        int guess;
        Scanner scanner = new Scanner(System.in);

        System.out.println("I have selected a number between 1 and 10. Try to guess it!");

        do {
            System.out.print("Enter your guess: ");
            while (!scanner.hasNextInt()) {
                System.out.println("That's not a valid number! Please try again.");
                scanner.next(); // discard invalid input
            }
            guess = scanner.nextInt();

            if (guess < secretNumber) {
                System.out.println("Too low, try again!");
            } else if (guess > secretNumber) {
                System.out.println("Too high, try again!");
            } else {
                System.out.println("Congratulations! You've guessed the number.");
            }
        } while (guess != secretNumber);

        scanner.close();
    }
}

```

整个过程我完全没有写一行 Java 代码，但是生成的代码运行下来完全没问题：

```shell
Welcome to the Puzzle Game!
I have selected a number between 1 and 10. Try to guess it!
Enter your guess: 7
Too high, try again!
Enter your guess: 5
Too high, try again!
Enter your guess: 3
Congratulations! You've guessed the number.
```

虽然这只是一个非常非常简单的 HelloWorld 程序，但真的能感受到在 AI 工具的加持下，生产力的图谱和提升已经到了另外一个层面。如今的程序员，除了分为 Junior Senior 之外，也许还可以分为会用 AI 的，和不会用 AI 的。

如果软件工程师已经如此，那么其他行业是不是也有这样的分野正在产生呢？
