<div align='justify'>

# Mat-Tree

>[Arquivos da valecard](https://v6.material.angular.dev/components/tree/overview)
>
>23 de Julho de 2025

## Overview

O mat-tree é pode ser construido no formato de flat tree ou nested tree. Flat-tree significa que no HTML os nós não ficam uns dentro dos outros, enquanto no nested tree os nós filhos precisam ficar dentro dos nós pais no HTML.

Flat tree:
<mat-tree>
  <mat-tree-node> parent node </mat-tree-node>
  <mat-tree-node> -- child node1 </mat-tree-node>
  <mat-tree-node> -- child node2 </mat-tree-node>
</mat-tree>

Nested tree:
<mat-tree>
   <mat-nested-tree-node>
     parent node
     <mat-nested-tree-node> -- child node1 </mat-nested-tree-node>
     <mat-nested-tree-node> -- child node2 </mat-nested-tree-node>
   </mat-nested-tree-node>
</mat-tree>



</div>
