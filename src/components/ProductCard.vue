<script setup lang="ts">
// 1. Modèle de données TypeScript d'un produit
export interface Produit {
  id: number;
  titre: string;
  prix: number;
  stock: number;
}

// 2. Déclaration des Props
// Le composant reçoit un objet "produit" conforme à l'interface
const props = defineProps<{
  produit: Produit;
}>();

// 3. Déclaration des Événements (Emits)
// Deux signaux que l'enfant peut envoyer au parent
const emit = defineEmits<{
  (e: 'acheter'): void;
  (e: 'supprimer'): void;
}>();
</script>

<template>
  <article
    style="
      border: 1px solid #e2e8f0;
      border-radius: 8px;
      padding: 16px;
      margin-bottom: 12px;
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
    "
  >
    <h3 style="margin-top: 0">{{ props.produit.titre }}</h3>
    <p>
      Prix : <strong>{{ props.produit.prix }} €</strong>
    </p>

    <!-- TODO 1 : Affichage conditionnel du stock -->
    <!-- Si stock > 0, afficher "Stock restant : X" -->
    <!-- Sinon (v-else), afficher "Rupture de stock" en rouge -->
    <p>
      <span v-if="props.produit.stock > 0"
        >Stock restant : {{ props.produit.stock }}</span
      >
      <span v-else style="color: #e53e3e; font-weight: bold"
        >Rupture de stock</span
      >
    </p>

    <div style="display: flex; gap: 8px">
      <!-- TODO 2 : Bouton Acheter -->
      <!-- - Désactiver le bouton si props.produit.stock === 0 avec :disabled="..." -->
      <!-- - Émettre l'événement 'acheter' au clic -->
      <button
        :disabled="props.produit.stock === 0"
        @click="emit('acheter')"
        style="padding: 6px 12px; cursor: pointer"
      >
        Ajouter au panier
      </button>

      <!-- TODO 3 : Bouton Supprimer -->
      <!-- - Émettre l'événement 'supprimer' au clic -->
      <button
        @click="emit('supprimer')"
        style="padding: 6px 12px; cursor: pointer; color: #e53e3e"
      >
        Supprimer
      </button>
    </div>
  </article>
</template>
