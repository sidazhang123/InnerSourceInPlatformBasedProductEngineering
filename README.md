# Inner Source in Platform-Based Product Engineering 内部开源在基于平台的产品中的实践研究

## @Authors: Dirk Riehle, Maximilian Capraro, Detlef Kips, and Lars Horn

# 摘要
内部开源（简称“内源”）是一种机构内跨部门用来创造共享的可复用资产的协作方式，有项目指出内源可促进代码复用及知识分享。
通过研究多个实际案例，我们分析了了三个大型软件开发公司在产品线工程中所遇到的问题。我们发现将作为利润中心的产品部门与作为成本中心的平台研发部门分开，是导致延期交付、故障率提升、组件冗余的一个根本原因。这三个机构均认为内源有助于解决这些问题，而本文分析了它们对于通过内源解决其自身问题的预期。最后，文章表明了我们对于这些公司该如何改变工程模式看法的结论。

# 一、简介：
内源软件开发指的是在公司内部软件开发中使用开源的最佳实践。因此，内源的协作要求参与者按自己意愿“贡献”而非“分配”工作、按照实际需要调整协作方式而非严格遵循预设的流程，并且根据事实结果而非参与者身份做出共同决定。

内源并不意味着要开发开源软件，而是要在开发中使用开源的最佳实践。许多公司现在都依赖于自顶向下的工作流程，而它们以为用这种自底向上的自组织方式改造下就可以增进生产力。本文重点在于公司内跨组织边界（尤其是大利润中心的边界）的软件开发。因为如果不能跨越这些部门边界，就完全无法进行该种协作。简言之，内源的目的就是串联各开发部门的“孤岛”从而实现协作。

惠普(HP)公司的Dinkelacker等人表示，实行内源可以改善产品质量、共享问题解决方案并更容易分配研发人力。Gurbani等人认为多人的协作可以提高质量，而公司内部可随意使用的软件组件能降低协作的成本。 IBM的Vitharana等人指出内源可以提升软件复用率。 除此以外，根据我们的经验，内源能更高效利用资源、改进软件质量以及提升开发速度。

过去的5年间，我们帮助了多个软件开发公司理解并采用内源。许多公司都发现按前文描述的来，实际上都难以实施。书上写的理论现实中却不起作用。本文将对3家曾尝试在“基于平台的产品工程”中使用内源的大型软件开发公司进行案例研究。平台是指一系列共享的可复用资产，包括但不限于软件库、组件和框架。而“基于平台的产品工程”是指用某共享的通用平台来构建一系列软件产品的工程。“产品线工程”是其中一个特例。

我们所调查的公司期望通过内源来帮助他们在资源缺乏、相关经验不足、需求不清的情况下所遇到的问题。然而，他们在实践内源时却遇到了麻烦。对此，本文要解决如下问题：
1.在目前的“基于平台的产品工程”中有什么问题（需要内源来解决）？
2.公司从使用内源中能得到什么收益？
3.公司在实践内源中遇到了什么问题？

本文所用使用的研究方法是多案例分析，收集分析的数据来自讨论会、正式访谈和材料阅读。研究过程及理论随着有效反馈的累计而推进及构建。
本文的贡献在于：
* 提供3个关于基于平台的产品工程的典型案例
* 为以上3个问题提出对应的解决办法

开源从基于志愿的、松散的软件开发模式（对所有人免费开放）发展到基于“基金会”的开发模式（受基金会管理），而我们也从案例研究中发现，内源同样应该遵循“受管理”的模式，而不是仅如本文开头所说的-共享出来就万事大吉。

本文将按如下结构进行论述：
第2部分 - 检视内源和产品线工程所采取的相关行动
第3部分 - 阐述我们研究所采取的设置、方法以及数据来源
第4部分 - 对于所研究的3个问题提出相应结论
第5部分 - 讨论我们的发现并对理论验证提出假设
第6部分 - 讨论现有方案的局限
第7部分 - 对未来的展望及重点回顾

# 二、相关工作

内源最开始由Dinkelacker等人在2002年研究提出，之后才有相关案例陆续出现。在基于平台的产品工程方面，“Software Product Lines: Practices and
Patterns”和“Software Product Line Engineering: Foundations, Principles and Techniques.”中所述的产品线工程得到了更多关注，因此我们主要关注这点。

**2.1 内源软件开发**

内源软件开发指的是在公司内部软件开发中使用开源的最佳实践，同时也有人称其为“混合开源”、“企业开源”、“公司内部开源”。内源是拓展公司现有的开发模式而不是颠覆它。
DTE Energy、Ericsson、HP、IBM、Kitware、Lucent、Nokia、Philips和SAP都在企业软件开发中使用内源。虽然这些使用报告没有回答我们的3个问题，但确实与一般的内源研究相关。

本文关注点在基于平台的产品开发中所设及的内源。而这些机构中除了Philips，没有其它关于该场景的案例。因此我们不能推断出Philips的问题和应对经验适用于其它基于平台的产品开发。 Philips在软件产品线工程中使用了内源的方法，发现其增进了开发人员的异地协作、跨部门协作，加强了知识管理和信息交换，通过使用方开发的补丁反而帮助解决平台自身瓶颈，并且提高软件质量和开发效率。 然而由于内部各组织流程不同，他们在实践内源时遇到了挑战。比较来自Philips的报告时我们发现，他们从内源中基本上获得的是那么几类好处，但在产品线工程的应用中却遇到很多挑战。相对于来自各个公司的主观描述报告，我们采取了定性的数据分析。我们的案例包含3个成熟的软件开发公司，而它们在公司文化上和组织形式上本质相同。我们通过排除全球化软件开发公司来降低分析的复杂度，因此我们的结论相较于公司的案例报告有显著高的有效性和可靠性。以绝对数字来看，对于内源的研究报告比实践案例还是少的。Melian、M€ahring以及Gaughan等人进行过探索性研究。他们讨论了实践内源所面对的收益及挑战。Stol等人提出了一种基于9个重要指标的模型来帮助实施内源，而该模型来自对文献的综合和对3个案例的分析。虽然一些关键因素旨在减少内源遇到的挑战，但该模型并不能指出使用内源的好处和挑战。而完全没有研究讨论在软件产品线工程中实践内源的细节。

Stol等人描述过一个正在发展软件产品线的未注名公司，他们指出了在产品线的内源道路上的13处挑战。我们可以证实他们的一些发现，但也得出了一些超出集成现有内源组件的结论。 我们研究了一个组件从计划、开发、使用到维护的全生命周期，并且使用了3个大型独立案例而非1个。因此我们相信我们的结论更广泛适用。

**2.2 基于平台的产品工程**

在研究中，我们调查了内源在基于平台的产品工程中的表现。大多数内源案例只展现了仅开发一个内源组件的短期工程。相比之下，我们讨论了包含产品组(case 1)、产品系列(case 2)和产品线(case 3)的三个案例，它们都是基于同一个提供着大量可复用资产的共享平台。产品线一词根据Clements和Northrop的定义是指一组软件密集型系统，它们共享一组共同的，受管理的功能，这些功能可以满足特定细分市场或任务的特定需求，并以规定的方式从一组共同的核心资产开发而成。该定义强调的是产物。Schwanninger等人认为：“软件产品线工程”表示支持有效开发此类软件密集型系统（或产品）的工程技术和实践的集合。第二个定义更强调过程而非产物，也因此与我们的工作更相符合。对于产品线工程的大量研究是关于管控产品可变性的工具和机制的。我们的工作相当于从另一个角度切入这些研究，因为我们专注于导致规范，开发和使用共享组件的过程，而不是用于管理它的工具和机制。

而且，产品线可变性的具体挑战也不是本研究关注的问题，因为我们的案例中，平台共享的可复用资产不仅要支持产品线，还要支持产品系列和产品组。

在已有的产品线工程术语中，领域工程流程控制可复用资产的识别，定义，创建和演化，这些资产通常作为应用程序或产品所基于的平台的一部分提供给应用程序。然后，在针对特定细分市场的应用程序情况中，应用程序工程过程控制可重用平台资产的选择，配置，改编和最终使用。 如果从更广泛的角度来看（不仅是产品线，还包括产品系列或产品组），我们的研究都与这些过程相关。具体来说，我们在研究中指出案例中公司在工程中遇到的问题，他们相信这些问题使用产品线方法无法解决，而只能使用内部来源方法。

产品线工程中的应用和领域工程过程存在的问题在业界已被认定，比如由Berger和Jepsen等人。在不称其为内源的情况下，该研究得出的结论与之前回顾的内源研究相似。内源与产品线工程之间的关系已被业界认可。 尤其值得注意的是，Van der Linden在第13届国际会议上就在产品线工程使用内源发表了教程。 然而这也只是一个从业者报告，我们尚无专门将内源与基于平台的产品工程/产品线工程结合在一起的研究。

# 三、研究方法

我们进行的是多案例研究。它是处理没有既定理论的现象的一种自然而然的选择，也是一种完善的探索性研究方法。

**3.1 案例选择（采样）**

我们从行业关系网中挑选用于案例学习的公司，它们在如下方面有着类似的特质：
* 在公共平台的基础上有着长期产品（运营10年以上）
* 在平台工程有着实践经验的成熟软件开发公司
* 组织规模足够大(包含至少500名开发者)
* 公司文化和组织关系上分布均匀，所有开发者处于同一工作地点

我们所有的案例均符合以上特点。这这使得它们在这些维度上具有可比性，从而使我们能够得出跨案例的结论并推展我们理论的广度。

值得注意的是，这种程度得聚焦也限制了我们结论的普适性，尤其是在本研究中，我们没有考虑跨国异地软件开发所设及的问题和应对方案。

**3.2公司案例**

这三个案例来自三个独立的、多元化的大型跨国软件产品公司。表1列出了这些公司及相关产品的关键属性。
公司1开发多种企业级软件产品，相应的case 1与某特定产品组有关；公司2提供多种产品的组合，相应case 2的主题是一个健康类的软件产品系列；
公司3跟2一样提供产品组合，而case3是关于电信运营商的软件产品线。
如前所述，我们不涉及跨国异地软件开发的复杂讨论。 而在分析过程中，我们才知道case 2需要与他人远程合作。 当我们进一步询问时，他们确信此信息与案例无关。
并非有意为之，但我们发现这三个案例有着相同的组织关系：
* 所有产品和支持平台均由一个业务部门拥有，并且由一个整体业务负责人负责所有产品。
* 业务部门分为产品部门，每个部门自己都是利润中心。 产品部门负责管理销售到特定市场的特定产品开发。 利润中心是可以直接为公司提供盈利的组织单位。 产品部门的经理背负其部门的盈利绩效。
* 提供可复用资产、支持平台运行的部门是成本中心，其成本由产品单位共同cover。 成本中心是一个单位中支持其它部门的单位，且公司不期望其直接提供盈利。
因此，我们根据组织架构指出了三种主要的不同分析粒度：整体业务部门，独立产品部门和平台部门。

![表1.案例中产品和所属公司的主要属性](https://raw.githubusercontent.com/sidazhang123/InnerSourceInPlatformBasedProductEngineering/master/table1.png)

**3.3数据的收集**

每个案例都是由案例研究合作伙伴提供。在case 1和2中，我们得以接触研究所设及的所有部门以及个人（产品组业务部门、我们选择的产品部门、平台部门）。在case 3中我们通过一个内部咨询小组来与相关部门有限接触。
在所有case中，都不允许录音。在case 1和2中，我们有2名人员参加，一人提问一人做笔记。在case 3中，只允许1人参加并记录。
总共，我们进行了至少一小时、共21次的半结构化访谈，参见表2。我们还收集了产品信息，内部备忘录，软件文档和组织文档，参见表3。
案例研究是按照编号顺序进行的。从case 1开始，我们与案例研究合作伙伴的代表一起完善了我们的访谈问题和观点，并据此选择性地进行后续访谈。
在case 2和3中，我们像在case 1中一样保持不变的主要问题和访谈准则但是此类研究的访谈是探索性的，因此我们允许理论上的敏感性，并进行了一些未在访谈准则中计划的讨论。
case 2重复了1中的大多数问题，而在案例3也没提供多少新信息，至此我们认为数据收集已经充分，可以停止访谈并得出结论。

**3.4 数据分析（基于“内容分析法”）**

我们执行了迭代式和增量式“定性”数据分析（QDA），使用定性数据分析工具MaxQDA。使用QDA进行理论构建的过程包括反复研究现有材料和新材料，注释（“编号”）文本段以及抽象出一个编号系统，即开发中理论的基础。
编号系统由编号按树状层次结构组成，在根节点附近有所谓的核心类别，而最具体的代码为叶子节点。 不同的活动以不同的方式改变层次结构。
“开放式编号”创建用于构建层次结构的基本编号，得到主要材料的直接注释，并直接链接到它们。
“枢纽编号”通过从开放式编号中派生出更多抽象概念和类别来构建这个编号系统，即为编号系统的生成支撑架构。
“选择性编号”可以让人选择重要的内容和不重要的内容。 通过删除无关紧要的部分，形成编号系统的理论核心。

编号系统中的概念节点由案例备忘节点相互链接在一起，以丰富概念本身和节点之间的关系，并强化最终结论和由主要论据而生的见解。我们使用了常量比较法来保证代码系统的内聚力，并关注在我们要解决的问题。

最终的编号系统和其中的案例备忘是本文理论的一个抽象表达，而我们最终由归纳法得到描述性的理论，他们适用于原案例的情况，但不一定普遍适用。

**3.5 质量保证**

这项工作是基于实验进行的，因此得出的理论有着较高的可信度。通常来讲，通过遵循一定的方法论可以保持理论的质量。我们让另一人构建了另一套编号系统，而这个独立开发的系统显示出与原始系统较高的一致性。 为了进行评估，我们一起仔细检查了两套系统，发现几乎没有矛盾之处，这显示出我们结论的可靠性和严谨性。我们所用的大量论据符合数据三角验证法(data triangulation)，这增加了我们理论的自洽性。

# 四、研究结果

本节介绍了基于平台的产品工程中应对特定问题的方案，将内源应用于此类产品工程后的预期收益以及实施时会遇到的挑战。

**4.1结果介绍**

本节将使用因果图，它能比传统自上而下的概念和关系讨论更好地展现我们的结论。在我们的图中，一个方框代表一个概念，而方框底部的数字表示所设及案例的编号。 灰色背景代表了这些概念的分类情况。
因果关系是从左向右展现的。 两个概念之间的箭头连接着原因和结果。 一个关系中的结果也可作为其它关系中的原因。 因果关系可能是多对多的，我们将这种关系称为非循环图。 因果关系是可传递的。 在我们的图中，省略了通过传递关系从别处派生而来的链接。
在全部三个案例的研究中，我们均不被允许录音。我们在以下各章节中的引述均来自笔记以及相应的总结或转述。 另外，我们将特定公司的术语改成通用的。

**4.2产品工程中的问题**

图1和图2给出了问题的因果图及其对案例中公司的影响。图1体现了组织结构方面的问题，图2显示了这些问题如何在相应领域影响了工作流程。 两张图中有些后果的起因相同，而我们将其拆开便于阅读。
主要分析结果如下：
根本原因是，将作为利润中心的产品部门与作为成本中心的平台部门分隔开，会使交付延竖井缓、交付质量降低和软件中组件冗余重复。
在我们的案例研究中，业务部门掌控着所有产品和平台，产品部门开发特定的产品，而平台部门通过共享可复用资产来支持产品部门的工作。 这些业务部门都在组织结构上被划分为作为利润中心的产品部门和作为成本中心的平台部门。
如图1所示，组织结构上的问题可以追溯到“将产品部门切分为利润中心，将平台部门切分为成本中心”，这使它们成为所谓的“孤岛”，而无法进行充分的协作。尤其是将产品部门独立作为利润中心会导致：
* “缺乏整体的业务视角”，即每个产品部门出于各自的利益行事，而无视协作可能产生的互利互惠。
* “产品部门之间的信任不足”，其他产品部门被视为威胁或竞争对手而不是潜在的合作者。
* “产品部门之间的权力斗争”，部分或全部产品部门的管理者无视其他产品部门的需求，只在努力维护自己的利益。
* “开发人员沟通不足”，即开发人员没有时间在公司内相互交流。

此外，由于利润中心只对自身盈利负责，它们在调用开发人员方面总是比成本中心有优势，这种切分方式会致使平台部门缺乏资源。
图1和图2没有展现出所有的因果关系，而讨论全部互动关系也超出了本文的合理范围。 因此，在以下各节中，我们重点关注以下三个主要的因果关系：

1.平台部门缺乏资源 -> 基于平台的产物无法及时交付 -> 产品无法及时交付
2.产品部门间的权斗 -> 不合理的需求优先级 -> 返工和资源浪费 -> 产品无法及时交付
3.部门间协作不足 -> 对其他部门了解有限 -> 对可复用资产的认识不到位 -> 可复用资产的质量缺陷 -> 产品质量下降

因为这些因果关系链在访谈中最多被提及，所以我们选择这些因果关系来阐述。

**4.2.1 因果关系1：资源不足**
