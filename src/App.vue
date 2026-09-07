<script setup lang="ts">
import { ref, computed } from 'vue';
import ProductCard, { type Produit } from './components/ProductCard.vue';

// Données initiales
const produits = ref<Produit[]>([
  { id: 1, titre: 'Écran 27" 4K', prix: 350, stock: 3 },
  { id: 2, titre: 'Souris sans fil', prix: 45, stock: 4 },
  { id: 3, titre: 'Clavier mécanique', prix: 110, stock: 0 },
]);

// Panier : stocke les prix des articles achetés
const panier = ref<number[]>([]);

// -------------------------------------------------------------
// TODO 1 : Calculer le total du panier avec computed()
// La variable doit s'appeler 'totalPanier'
// Elle doit renvoyer la somme des nombres contenus dans panier.value
// -------------------------------------------------------------
const totalPanier = computed<number>(() => {
  return panier.value.reduce((total, prix) => total + prix, 0);
});

// -------------------------------------------------------------
// TODO 2 : Fonction gererAchat(produit: Produit)
// - Vérifier que le stock du produit est strictement supérieur à 0
// - Si oui : décrémenter son stock de 1
// - Et ajouter son prix au tableau panier.value
// -------------------------------------------------------------
function gererAchat(produit: Produit)  {
  if (produit.stock > 0) {
    produit.stock -= 1
    panier.value.push(produit.prix)
  }
}

// -------------------------------------------------------------
// TODO 3 : Fonction gererSuppression(idProduit: number)
// - Retirer le produit correspondant de la liste produits.value
// -------------------------------------------------------------
</script>

<template>
  <main
    style="
      padding: 2rem;
      font-family: sans-serif;
      max-width: 650px;
      margin: 0 auto;
    "
  >
    <h1>Ma Boutique en Ligne</h1>

    <!-- Bannière récapitulative -->
    <section
      style="
        background: #edf2f7;
        padding: 12px 16px;
        border-radius: 8px;
        margin-bottom: 24px;
      "
    >
      <p style="margin: 0; font-size: 1.1rem">
        <!-- TODO 4 : Afficher ici le nombre d'articles (longueur de panier) -->
        🛒 Articles au panier : <strong>0</strong> |
        <!-- TODO 5 : Afficher ici le total calculé par totalPanier -->
        Total : <strong>0 €</strong>
      </p>
    </section>

    <!-- Liste des produits -->
    <section>
      <h2>Articles disponibles</h2>

      <!-- --------------------------------------------------------
        TODO 6 : Afficher chaque produit avec le composant <ProductCard />
        - Boucler avec v-for sur le tableau 'produits'
        - Ne pas oublier :key
        - Passer la prop :produit
        - Écouter l'événement @acheter pour appeler gererAchat(...)
        - Écouter l'événement @supprimer pour appeler gererSuppression(...)
      --------------------------------------------------------- -->
    </section>
  </main>
</template>
