<script>
    import virusImg from "$lib/assets/virus.png";
    import bacteriumImg from "$lib/assets/bacterium.png";
    import fungusImg from "$lib/assets/fungus.png";
    import feverImg from "$lib/assets/fever.png";
    import hungryImg from "$lib/assets/hungry.png";
    import spreeImg from "$lib/assets/spree.png";
    import mutationImg from "$lib/assets/mutation.png";
    import painImg from "$lib/assets/pain.png";
    import analgesicImg from "$lib/assets/analgesic.png";
    import antibacteriumImg from "$lib/assets/antibacterium.png";
    import antifungusImg from "$lib/assets/antifungus.png";
    import antivirusImg from "$lib/assets/antivirus.png";
    import antipyreticImg from "$lib/assets/antipyretic.png";
    import checkupImg from "$lib/assets/checkup.png";
    import hygieneImg from "$lib/assets/hygiene.png";
    import lifeImg from "$lib/assets/life.png";
    import restImg from "$lib/assets/rest.png";
    import vaccineImg from "$lib/assets/vaccine.png";
    import vitaminImg from "$lib/assets/vitamin.png";

    const imagesSrc = {
        virus: virusImg,
        bacterium: bacteriumImg,
        fungus: fungusImg,
        fever: feverImg,
        hungry: hungryImg,
        spree: spreeImg,
        mutation: mutationImg,
        pain: painImg,
        analgesic: analgesicImg,
        antibacterium: antibacteriumImg,
        antifungus: antifungusImg,
        antivirus: antivirusImg,
        antipyretic: antipyreticImg,
        checkup: checkupImg,
        hygiene: hygieneImg,
        life: lifeImg,
        rest: restImg,
        vaccine: vaccineImg,
        vitamin: vitaminImg,
    };
</script>

<p>
    Neste jogo cada jogador recebe um deck específico de 44 cartas.<br />
    As cartas do invasor representam as doenças e situações adversas. As cartas do
    defensor representam os tratamentos e remediações para as situações e doenças
    que aparecem ao longo do jogo.<br />
    Na primeira rodada o jogador saca 5 cartas do deck, a cada rodada 1 carta é puxada
    do deck automaticamente e pelo menos 1 carta deve ser colocada na mesa.<br
    />
    O invasor deve iniciar o primeiro turno escolhendo a carta para ser colcoada
    na mesa. <br />
    Para cada jogador no máximo 5 cartas podem estar na mesa simultaneamente.<br
    />
    Quando uma carta vai para a mesa seu efeito passa a valer.<br />
    Uma carta de defesa será ativada quando ela for revelada.<br />
    Uma vez ativada, uma carta de defesa deixa a mesa e vai para o cemitério.<br
    />
    Uma carta de ataque deixará a mesa e seguirá para o cemitério caso uma carta
    de defesa compatível seja ativada.<br />
    O total de pontos de vida do defensor é 100.<br />
    Caso o invasor fique sem cartas em seu deck o defensor vence o jogo.<br />
    Caso o defensor fique sem pontos de vida antes do fim do deck do invasor, o invasor
    vence o jogo.<br />
    As cartas do invasor são as pretas.<br />
    As cartas do defensor são as azuis.<br />
</p>
<figure>
    <p>
        <img src={virusImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            8 cartas com dano inicial variando entre 1 e 4.<br />
            A cada rodada o dano cresce em progressão aritmética.
        </figcaption>
    </p>
    <p>
        <img src={bacteriumImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            8 cartas com dano inicial variando entre 1 e 4.<br />
            A cada rodada o dano cresce em progressão aritmética.
        </figcaption>
    </p>
    <p>
        <img src={fungusImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            8 cartas com dano inicial variando entre 1 e 4.<br />
            A cada rodada o dano cresce em progressão aritmética.
        </figcaption>
    </p>
    <p>
        <img src={feverImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            4 cartas.<br />
            Dobra o dano de uma doença.
        </figcaption>
    </p>
    <p>
        <img src={hungryImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            4 cartas.<br />
            Dobra o dano de uma doença.
        </figcaption>
    </p>
    <p>
        <img src={spreeImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            4 cartas.<br />
            Dobra o dano de uma doença.
        </figcaption>
    </p>
    <p>
        <img src={mutationImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            4 cartas.<br />
            Transforma o dano de uma doença para progressão geométrica.
        </figcaption>
    </p>
    <p>
        <img src={painImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            4 cartas. <br />
            Dobra o dano de uma doença.
        </figcaption>
    </p>
    <p>
        <img src={analgesicImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            4 cartas. <br />
            Elimina a dor.
        </figcaption>
    </p>
    <p>
        <img src={antibacteriumImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            4 cartas. <br />
            Elimina uma doença bacteriana.
        </figcaption>
    </p>
    <p>
        <img src={antivirusImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            4 cartas. <br />
            Elimina uma doença viral.
        </figcaption>
    </p>
    <p>
        <img src={antipyreticImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            4 cartas. <br />
            Elimina a febre.
        </figcaption>
    </p>
    <p>
        <img src={checkupImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            2 cartas. <br />
            Mostra todas as cartas do atacante que estão viradas para baixo.<br
            />
            Jogando com o invasor ela vira todas as cartas do invasor para baixo.
        </figcaption>
    </p>
    <p>
        <img src={hygieneImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            4 cartas. <br />
            Reduz o dano de uma doença pela metade.
        </figcaption>
    </p>
    <p>
        <img src={lifeImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            2 cartas. <br />
            Aumenta 10 pontos de vida.
        </figcaption>
    </p>
    <p>
        <img src={restImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            4 cartas. <br />
            Elimina a farra.
        </figcaption>
    </p>
    <p>
        <img src={vaccineImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            8 cartas. <br />
            Elimina uma doença viral ou bacteriana.
        </figcaption>
    </p>
    <p>
        <img src={vitaminImg} width="136" height="200" alt="Virus" />
        <!-- svelte-ignore a11y-structure -->
        <figcaption>
            4 cartas. <br />
            Elimina a fome.
        </figcaption>
    </p>
</figure>
