<script>
    import Card from '$lib/Card.svelte';
    import virusImg from '$lib/assets/virus.png';
    import bacteriumImg from '$lib/assets/bacterium.png';
    import fungusImg from '$lib/assets/fungus.png';
    import feverImg from '$lib/assets/fever.png';
    import hungryImg from '$lib/assets/hungry.png';
    import spreeImg from '$lib/assets/spree.png';
    import mutationImg from '$lib/assets/mutation.png';
    import painImg from '$lib/assets/pain.png';



    let playerDeck = Array.from({length: 40}, () => Math.floor(Math.random() * 40));

</script>

<!-- <Card imgAlt="virus"  {imgSrc} isCovered={x}>

</Card>

<Card imgAlt="virus"  {imgSrc} isCovered={!x}>

</Card>
 -->



