<div align='justify'>

# Mat-Tree

>[Arquivos da valecard](https://v6.material.angular.dev/components/tree/overview)
>
>23 de Julho de 2025

## Overview

O mat-tree é pode ser construido no formato de flat tree ou nested tree. Flat-tree significa que no HTML os nós não ficam uns dentro dos outros, enquanto no nested tree os nós filhos precisam ficar dentro dos nós pais no HTML.

Flat tree:
```html
<mat-tree>
  <mat-tree-node> parent node </mat-tree-node>
  <mat-tree-node> -- child node1 </mat-tree-node>
  <mat-tree-node> -- child node2 </mat-tree-node>
</mat-tree>
```
Nested tree:
```html
<mat-tree>
   <mat-nested-tree-node>
     parent node
     <mat-nested-tree-node> -- child node1 </mat-nested-tree-node>
     <mat-nested-tree-node> -- child node2 </mat-nested-tree-node>
   </mat-nested-tree-node>
</mat-tree>
```
## Analisando o exemplo do chatgpt

```ts
import { Component } from '@angular/core';
import { FlatTreeControl } from '@angular/cdk/tree';
import { MatTreeFlatDataSource, MatTreeFlattener } from '@angular/material/tree';

interface FoodNode {
  name: string;
  children?: FoodNode[];
}

interface FlatNode {
  name: string;
  level: number;
  expandable: boolean;
}

@Component({
  selector: 'tree-basic',
  templateUrl: 'tree-basic.component.html',
  styleUrls: ['tree-basic.component.css']
})
export class TreeBasicComponent {
  private TREE_DATA: FoodNode[] = [
    {
      name: 'Fruits',
      children: [
        { name: 'Apple' },
        { name: 'Banana' }
      ]
    },
    {
      name: 'Vegetables',
      children: [
        { name: 'Tomato' },
        { name: 'Potato' }
      ]
    }
  ];

  treeControl = new FlatTreeControl<FlatNode>(
    node => node.level,
    node => node.expandable
  );

  treeFlattener = new MatTreeFlattener<FoodNode, FlatNode>(
    (node: FoodNode, level: number): FlatNode => ({
      name: node.name,
      level,
      expandable: !!node.children && node.children.length > 0
    }),
    node => node.level,
    node => node.expandable,
    node => node.children
  );

  dataSource = new MatTreeFlatDataSource(this.treeControl, this.treeFlattener);

  constructor() {
    this.dataSource.data = this.TREE_DATA;
  }

  hasChild = (_: number, node: FlatNode) => node.expandable;
}
```

Primeiro ele cria uma interface para o nó pai:

```ts
interface FoodNode {
  name: string;
  children?: FoodNode[];
}
```

Depois cria uma interface para o nó filho:

```ts
interface FlatNode {
  name: string;
  level: number;
  expandable: boolean;
}
```

Em seguida ele cria uns dados de exemplo, que são nada mais que uma lista de nós pais com nós filhos:

```ts
  private TREE_DATA: FoodNode[] = [
    {
      name: 'Fruits',
      children: [
        { name: 'Apple' },
        { name: 'Banana' }
      ]
    },
    {
      name: 'Vegetables',
      children: [
        { name: 'Tomato' },
        { name: 'Potato' }
      ]
    }
  ];
```

Depois ele define o `treeControl`, basicamente informando que as informações de level do nó e se ele se expande ou não (se é pai ou não) podem ser encontradas no próprio atributo do objeto.

```ts
  treeControl = new FlatTreeControl<FlatNode>(
    node => node.level,
    node => node.expandable
  );
```

</div>
