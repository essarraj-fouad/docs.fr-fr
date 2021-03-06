---
title: "Vue d&#39;ensemble des animations de trac&#233;s | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "animation, les chemins d’accès"
  - "animations de tracés"
ms.assetid: 979c732c-df74-47a6-be96-8e07b3707d53
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Vue d&#39;ensemble des animations de trac&#233;s
<a name="introduction"></a>Cette rubrique présente des animations de tracé qui vous permettent d’utiliser un tracé géométrique pour générer des valeurs de sortie. Les animations de tracé sont utiles pour déplacer et faire pivoter des objets sur des tracés complexes.  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>Conditions préalables  
 Pour comprendre cette rubrique, vous devez être familiarisé avec [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] les fonctionnalités des animations. Pour une introduction aux fonctionnalités d’animation, consultez le [vue d’ensemble de l’Animation](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
 Étant donné que vous utilisez un <xref:System.Windows.Media.PathGeometry> objet pour définir une animation de tracé, vous devez également être familiarisé avec <xref:System.Windows.Media.PathGeometry> et les différents types de <xref:System.Windows.Media.PathSegment> objets. Pour plus d’informations, consultez la [Geometry Overview](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md).  
  
<a name="what_is_a_path_animation"></a>   
## <a name="what-is-a-path-animation"></a>Qu’est une Animation de tracé ?  
 Une animation de tracé est un type de <xref:System.Windows.Media.Animation.AnimationTimeline> qui utilise un <xref:System.Windows.Media.PathGeometry> comme entrée. Au lieu de définir un From, de propriété, ou par (comme vous le feriez pour un From/To/By animation) ou à l’aide d’images clés (que vous utilisez pour une animation d’image clé), vous définissez un tracé géométrique et utilisez-le pour définir le `PathGeometry` propriété de l’animation de chemin d’accès. En tant que passe le chemin d’accès, il lit x, y et informations d’angle dans le chemin d’accès et utilise ces informations pour générer sa sortie.  
  
 Animations de tracés sont très utiles pour animer un objet sur un tracé complexe. Pour déplacer un objet sur un tracé est d’utiliser un <xref:System.Windows.Media.MatrixTransform> et un <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> pour transformer un objet sur un tracé complexe. L’exemple suivant illustre cette technique à l’aide de la <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> objet à animer le <xref:System.Windows.Media.MatrixTransform.Matrix%2A> propriété d’un <xref:System.Windows.Media.MatrixTransform>. Le <xref:System.Windows.Media.MatrixTransform> est appliqué à un bouton et permet de déplacer sur un tracé courbé. Étant donné que la <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.DoesRotateWithTangent%2A> est définie sur `true`, le rectangle pivote sur la tangente du chemin d’accès.  
  
 [!code-xml[PathAnimationGallery_snippet#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/matrixanimationusingpathdoesrotatewithtangentexample.xaml#matrixanimationusingpathdoesrotatewithtangentwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/MatrixAnimationUsingPathDoesRotateWithTangentExample.cs#matrixanimationusingpathdoesrotatewithtangentwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/MatrixAnimationUsingPathDoesRotateWithTangentExample.vb#matrixanimationusingpathdoesrotatewithtangentwholepage)]  
  
 Pour plus d’informations sur la syntaxe de chemin d’accès qui est utilisée dans le [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] exemple, consultez la [Path Markup Syntax](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md) vue d’ensemble. Pour l’exemple complet, consultez la page [exemple d’Animation de chemin d’accès](http://go.microsoft.com/fwlink/?LinkID=160028).  
  
 Vous pouvez appliquer une animation de chemin d’accès à une propriété à l’aide un <xref:System.Windows.Media.Animation.Storyboard> dans [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] et du code, ou en utilisant la <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> méthode dans le code. Vous pouvez également utiliser une animation de tracé pour créer un <xref:System.Windows.Media.Animation.AnimationClock> et l’appliquer à une ou plusieurs propriétés. Pour plus d’informations sur les différentes méthodes pour appliquer des animations, consultez [Property Animation Techniques Overview](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md).  
  
<a name="animation_types"></a>   
## <a name="path-animation-types"></a>Types d’animations de chemin d’accès  
 Étant donné que les animations génèrent des valeurs de propriété, il existe différents types d’animations pour différents types de propriété. Pour animer une propriété qui prend un <xref:System.Double> (telles que la <xref:System.Windows.Media.TranslateTransform.X%2A> propriété d’un <xref:System.Windows.Media.TranslateTransform>), utilisez une animation qui produit des <xref:System.Double> valeurs. Pour animer une propriété qui accepte un <xref:System.Windows.Point>, utilisez une animation qui produit des <xref:System.Windows.Point> valeurs et ainsi de suite.  
  
 Classes d’animation de tracé appartiennent à la <xref:System.Windows.Media.Animation> espace de noms et la convention d’affectation de noms suivante :  
  
 *<>\>*`AnimationUsingPath`  
  
 Où * <> \> * est le type de valeur que la classe anime.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]fournit le chemin d’accès suivant de classes d’animation.  
  
|Type de propriété|Classe d’animation de chemin d’accès correspondant|Exemple|  
|-------------------|----------------------------------------|-------------|  
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>|[Animer un objet sur un tracé (Animation Double)](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-an-object-along-a-path-double-animation.md)|  
|<xref:System.Windows.Media.Matrix>|<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>|[Animer un objet sur un tracé (Animation de matrice)](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-an-object-along-a-path-matrix-animation.md)|  
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimationUsingPath>|[Animer un objet sur un tracé (Animation de Point)](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-an-object-along-a-path-point-animation.md)|  
  
 A <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> génère <xref:System.Windows.Media.Matrix> les valeurs de ses <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.PathGeometry%2A>. Lorsqu’il est utilisé avec un <xref:System.Windows.Media.MatrixTransform>, un <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> peut déplacer un objet sur un chemin d’accès. Si vous définissez la <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.DoesRotateWithTangent%2A> propriétés de la <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> à `true`, il fait également pivoter l’objet sur les courbes du chemin d’accès.  
  
 A <xref:System.Windows.Media.Animation.PointAnimationUsingPath> génère <xref:System.Windows.Point> les valeurs de coordonnées x et y de son <xref:System.Windows.Media.Animation.PointAnimationUsingPath.PathGeometry%2A>. En utilisant un <xref:System.Windows.Media.Animation.PointAnimationUsingPath> pour animer une propriété qui accepte <xref:System.Windows.Point> valeurs, vous pouvez déplacer un objet sur un chemin d’accès. A <xref:System.Windows.Media.Animation.PointAnimationUsingPath> ne peut pas faire pivoter des objets.  
  
 A <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> génère <xref:System.Double> les valeurs de ses <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath.PathGeometry%2A>. En définissant le <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath.Source%2A> propriété, vous pouvez spécifier si les <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> utilise la coordonnée x, ordonnée ou angle du tracé comme sortie. Vous pouvez utiliser un <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> pour faire pivoter un objet ou le déplacer sur l’axe x ou l’axe des y.  
  
<a name="pathanimationinput"></a>   
## <a name="path-animation-input"></a>Entrée de l’Animation de chemin d’accès  
 Chaque classe d’animation de tracé fournit une <xref:System.Windows.Media.PathGeometry> propriété pour spécifier son entrée. L’animation de tracé utilise le <xref:System.Windows.Media.PathGeometry> pour générer ses valeurs de sortie. Le <xref:System.Windows.Media.PathGeometry> classe vous permet de décrire plusieurs illustrations complexes composées d’arcs, de courbes et de lignes.  
  
 Au cœur d’un <xref:System.Windows.Media.PathGeometry> est une collection de <xref:System.Windows.Media.PathFigure> objets, ces objets sont nommés ainsi car chaque illustration décrit une forme discrète le <xref:System.Windows.Media.PathGeometry>. Chaque <xref:System.Windows.Media.PathFigure> se compose d’un ou plusieurs <xref:System.Windows.Media.PathSegment> objets, décrivant chacun un segment de l’illustration.  
  
 Il existe de nombreux types de segments.  
  
|Type de segment|Description|  
|------------------|-----------------|  
|<xref:System.Windows.Media.ArcSegment>|Crée un arc elliptique entre deux points.|  
|<xref:System.Windows.Media.BezierSegment>|Crée une courbe de Bézier cubique entre deux points.|  
|<xref:System.Windows.Media.LineSegment>|Crée une ligne entre deux points.|  
|<xref:System.Windows.Media.PolyBezierSegment>|Crée une série de courbes de Bézier cubiques.|  
|<xref:System.Windows.Media.PolyLineSegment>|Crée une série de lignes.|  
|<xref:System.Windows.Media.PolyQuadraticBezierSegment>|Crée une série de courbes de Bézier quadratiques.|  
|<xref:System.Windows.Media.QuadraticBezierSegment>|Crée une courbe de Bézier quadratique.|  
  
 Les segments dans un <xref:System.Windows.Media.PathFigure> sont combinés en une forme géométrique unique qui utilise le point de terminaison d’un segment comme point de départ du segment suivant. Le <xref:System.Windows.Media.PathFigure.StartPoint%2A> propriétés d’un <xref:System.Windows.Media.PathFigure> Spécifie le point à partir de laquelle le premier segment est dessiné. Chaque segment suivant démarre au point de terminaison du segment précédent. Par exemple, une ligne verticale de `10,50` à `10,150` peut être défini en définissant le <xref:System.Windows.Media.PathFigure.StartPoint%2A> propriété `10,50` et la création d’un <xref:System.Windows.Media.LineSegment> avec un <xref:System.Windows.Media.LineSegment.Point%2A> paramètre de propriété `10,150`.  
  
 Pour plus d’informations sur <xref:System.Windows.Media.PathGeometry> , voir la [Geometry Overview](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md).  
  
 Dans [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], vous pouvez également utiliser une syntaxe abrégée spéciale pour définir la <xref:System.Windows.Media.PathGeometry.Figures%2A> propriétés d’un <xref:System.Windows.Media.PathGeometry>. Pour plus d’informations, consultez [Path Markup Syntax](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md) vue d’ensemble.  
  
 Pour plus d’informations sur la syntaxe de chemin d’accès qui est utilisée dans le [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] exemple, consultez la [Path Markup Syntax](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md) vue d’ensemble.  
  
## <a name="see-also"></a>Voir aussi  
 [Exemple d’Animation de chemin d’accès](http://go.microsoft.com/fwlink/?LinkID=160028)   
 [Syntaxe de balisage de chemin d’accès](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md)   
 [Rubriques "Comment" Animation de chemin d’accès](../../../../docs/framework/wpf/graphics-multimedia/path-animation-how-to-topics.md)   
 [Présentation de l’animation](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Propriété Animation Techniques Overview.](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)