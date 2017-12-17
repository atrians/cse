---
title: ":ramen: Google Classroom"
layout: post
date: 2017-12-12 20:00
tag: jekyll
image: https://koppl.in/indigo/assets/images/jekyll-logo-light-solid.png
headerImage: true
projects: true
hidden: true # don't count this post in blog pagination
description: "This is a simple and minimalist template for Jekyll for those who likes to eat noodles."
category: project
author: johndoe
externalLink: false
---

<body>
<div id="content">
<h1 class="title">Computer Network Laboratory</h1>

<div id="outline-container-orgec66cf5" class="outline-2">
<h2 id="orgec66cf5"><span class="section-number-2">1</span> Bellman Ford</h2>
<div class="outline-text-2" id="text-1">
<div class="org-src-container">
<pre class="src src-C++"><span style="color: #228b22;">import</span> <span style="color: #a0522d;">java</span>.util.Scanner;

<span style="color: #a020f0;">public</span> <span style="color: #a020f0;">class</span> <span style="color: #228b22;">BellmanFord</span> {
    <span style="color: #228b22;">int</span> <span style="color: #a0522d;">n</span>;
    <span style="color: #228b22;">int</span>[][] a;
    <span style="color: #228b22;">int</span>[]   d;
    <span style="color: #228b22;">int</span>[]   p;
    <span style="color: #228b22;">int</span> <span style="color: #a0522d;">s</span>;
    <span style="color: #a020f0;">public</span> <span style="color: #a020f0;">final</span> <span style="color: #a020f0;">static</span> <span style="color: #228b22;">int</span> INFTY=999;

    <span style="color: #0000ff;">BellmanFord</span>(<span style="color: #228b22;">int</span> <span style="color: #a0522d;">n</span>)
    {
        <span style="color: #a020f0;">this</span>.n = n;

        a = <span style="color: #a020f0;">new</span> <span style="color: #228b22;">int</span>[n][n];
        d = <span style="color: #a020f0;">new</span> <span style="color: #228b22;">int</span>[n];
        p = <span style="color: #a020f0;">new</span> <span style="color: #228b22;">int</span>[n];
    }

    <span style="color: #228b22;">void</span> <span style="color: #0000ff;">bellmanFord</span>()
    {
        <span style="color: #b22222;">// </span><span style="color: #b22222;">Initialization</span>
        <span style="color: #a020f0;">for</span>(<span style="color: #228b22;">int</span> <span style="color: #a0522d;">i</span>=0; i &lt; n; i++)
        {
            d[i] = a[s][i];
            p[i] = a[s][i] == INFTY ? -1 : s;
        }
        p[s] = -1;

        <span style="color: #a020f0;">for</span>(<span style="color: #228b22;">int</span> <span style="color: #a0522d;">i</span>=0; i &lt; n-1; i++)
        {
            <span style="color: #b22222;">// </span><span style="color: #b22222;">Relax all edges iteratively (n-1) times</span>
            <span style="color: #a020f0;">for</span>(<span style="color: #228b22;">int</span> <span style="color: #a0522d;">u</span>=0; u &lt; n; u++)
            {
                <span style="color: #a020f0;">for</span>(<span style="color: #228b22;">int</span> <span style="color: #a0522d;">v</span>=0; v &lt; n; v++)
                {
                    <span style="color: #a020f0;">if</span>(d[v] &gt; d[u]+a[u][v])
                    {
                        d[v] = d[u]+a[u][v];
                        p[v] = u;
                    }
                }
            }
        }
    }

    <span style="color: #228b22;">void</span> <span style="color: #0000ff;">input</span>(<span style="color: #228b22;">Scanner</span> <span style="color: #a0522d;">scanner</span>)
    {
        System.out.println(<span style="color: #8b2252;">"Enter G: "</span>);

        <span style="color: #a020f0;">for</span>(<span style="color: #228b22;">int</span> <span style="color: #a0522d;">i</span>=0; i&lt;n; i++)
        {   
            <span style="color: #a020f0;">for</span>(<span style="color: #228b22;">int</span> <span style="color: #a0522d;">j</span>=0; j&lt;n; j++)
            {
                a[i][j] = scanner.nextInt();
                <span style="color: #a020f0;">if</span> (i != j &amp;&amp; a[i][j] == 0) a[i][j] = INFTY;
            }
        }

        System.out.print(<span style="color: #8b2252;">"Enter the source vertex: "</span>);
        s = scanner.nextInt();

        scanner.close();
    }

    <span style="color: #228b22;">void</span> <span style="color: #0000ff;">path</span>(<span style="color: #228b22;">int</span> <span style="color: #a0522d;">v</span>)
    {
        <span style="color: #a020f0;">if</span> (v == -1) <span style="color: #a020f0;">return</span>;

        path(p[v]);
        System.out.print(<span style="color: #8b2252;">"."</span>+v);
    }

    <span style="color: #228b22;">void</span> <span style="color: #0000ff;">output</span>()
    {
        <span style="color: #228b22;">int</span> <span style="color: #a0522d;">i</span>;

        <span style="color: #a020f0;">for</span>(i=0; i &lt; n; i++)
        {
            System.out.print(<span style="color: #8b2252;">"d("</span> + s + <span style="color: #8b2252;">","</span> + i + <span style="color: #8b2252;">")="</span> + d[i]+<span style="color: #8b2252;">" :p"</span>);
            path(i);
            System.out.println();
        }
    }

    <span style="color: #a020f0;">public</span> <span style="color: #a020f0;">static</span> <span style="color: #228b22;">void</span> main(String[] args) {
        <span style="color: #228b22;">int</span>         <span style="color: #a0522d;">n</span>;
        <span style="color: #228b22;">Scanner</span> <span style="color: #a0522d;">scanner</span> = <span style="color: #a020f0;">new</span> <span style="color: #228b22;">Scanner</span>(System.in);

        System.out.print(<span style="color: #8b2252;">"Enter n: "</span>);
        n = scanner.nextInt();

        <span style="color: #228b22;">BellmanFord</span> <span style="color: #a0522d;">bf</span> = <span style="color: #a020f0;">new</span> <span style="color: #228b22;">BellmanFord</span>(n);

        bf.input(scanner);
        bf.bellmanFord();
        bf.output();
    }
}


</pre>
</div>
</div>
</div>
</div>
<div id="postamble" class="status">
<p class="author">Author: by G. Srinivasachar and Archana J N</p>
<p class="date">Created: 2017-12-17 Sun 13:17</p>
<p class="validation"><a href="http://validator.w3.org/check?uri=referer">Validate</a></p>
</div>
</body>

