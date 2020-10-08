---
title: "Recommending Library Migration Target via Mining Dependency Change Sequences"
collection: publications
permalink: /publication/2021-recommending-library-migration
excerpt: 'The wide adoption of third-party libraries in software projects is beneficial but also risky. Third party libraries may have security vulnerabilities, may be abandoned by their maintainers, or may no longer align with current project requirements. Under such circumstances, a software project needs to migrate its library to another library with similar functionalities, but it is often not easy to find good substitute libraries and make migration decisions between candidate libraries. Therefore, automated recommendation of migration target is desired to support decision making in library migration. However, existing library migration mining methods suffer from low performance and require extensive human effort to correct the results.
In this paper, we present a recommendation approach for library migration through mining dependency change sequences of existing software repositories. Given a library to migrate, our approach first generate candidate libraries from the sequences, and then rank them using four carefully designed metrics to capture right migration targets from large number of candidates: Rule Support, Message Support, Distance Support and API Support. We evaluate our approach on 21,358 Java GitHub projects and 773 manually confirmed migration rules from previous work.  The experiments show that our metrics can effectively separate real migration targets from other libraries, and our approach significantly outperforms existing works, with MRR of 0.8566, top-1 precision of 0.7947, top-10 NDCG of 0.7665 and top-20 recall of 0.8939. We also evaluate our approach on 480 libraries not included in previous work, where we successfully confirm 661 new migration rules. The demo, source code and data are provided at: \Fix{TODO: Add a link here}'
date: 2020-10-22
venue: 'Under Review'
paperurl: 'Not Available'
citation: '<b>Hao He</b>, Yulin Xu, Yifei Xu, Yixiao Ma, Guangtai Liang and Minghui Zhou. Recommending Library Migration Target via Mining Dependency Change Sequence. Under Review.'
---

## Abstract

The wide adoption of third-party libraries in software projects is beneficial but also risky. 
Third party libraries may have security vulnerabilities, may be abandoned by their maintainers, or may no longer align with current project requirements. 
Under such circumstances, a software project needs to migrate its library to another library with similar functionalities, but it is often not easy to find good substitute libraries and make migration decisions between candidate libraries. 
Therefore, automated recommendation of migration target is desired to support decision making in library migration.
However, existing library migration mining methods suffer from low performance and require extensive human effort to correct the results.

In this paper, we present a recommendation approach for library migration through mining dependency change sequences of existing software repositories.
Given a library to migrate, our approach first generate candidate libraries from the sequences, and then rank them using four carefully designed metrics to capture right migration targets from large number of candidates: Rule Support, Message Support, Distance Support and API Support.
We evaluate our approach on 21,358 Java GitHub projects and 773 manually confirmed migration rules from previous work. 
The experiments show that our metrics can effectively separate real migration targets from other libraries, and our approach significantly outperforms existing works, with MRR of 0.8566, top-1 precision of 0.7947, top-10 NDCG of 0.7665 and top-20 recall of 0.8939. 
We also evaluate our approach on 480 libraries not included in previous work, where we successfully confirm 661 new migration rules.
The demo, source code and data are provided at: \Fix{TODO: Add a link here}


[Download Paper Here](http://hehao98.github.io/files/2021-migration.pdf)

