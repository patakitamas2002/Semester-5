# 10.18.: ZH (fasza)

- Alakzatok rajzolása, színezése (kitöltése adott esetben), pozícionálása
- Raszteres algoritmusok (DDA, kód kiegészítés ~~vagy pszeudókód~~)
- Vágó algoritmus (Cohen-Sutherland leghosszabb változat)
- Bezier görbe algoritmusa (Kód kiegészítés + algoritmus működése)
  
```
ELJÁRÁS COHEN_SUTH_VAZL(PONT P0, PONT P1)
    VÁLTOZÓK
        EGÉSZ: KOD0, KOD1, KOD_KINN, X, Y;
        LOGIKAI: ELFOGAD;
    ALGORITMUS
        KOD0 <- VEGPONT_KOD(P0);
        KOD1 <- VEGPONT_KOD(P1);
        ELFOGAD <- HAMIS;
        CIKLUS_AMÍG (IGAZ)
            HA ((KOD0 VAGY KOD1) = HAMIS) AKKOR
                ELFOGAD <- IGAZ;
                CIKLUS_KILÉP;
            KÜLÖNBEN
                HA ((KOD0 ÉS KOD1) = IGAZ) AKKOR
                    CIKLUS_KILÉP;
                KÜLÖNBEN
                    HA (KOD0 = IGAZ) AKKOR
                        KOD_KINN <- KOD0;
                    KÜLÖNBEN
                        KOD_KINN <- KOD1;
                    HA_VÉGE;

                    HA ((KOD_KINN ÉS 1) = IGAZ) AKKOR
                        X <- ABLAK.BAL;
                        Y <- P0.Y + (P1.Y – P0.Y) * (ABLAK.BAL – P0.X) / (P1.X – P0.X);
                    KÜLÖNBEN
                        HA ((KOD_KINN ÉS 2) = IGAZ) AKKOR
                            X <- ABLAK.JOBB;
                            Y <- P0.Y + (P1.Y – P0.Y) * (ABLAK.JOBB – P0.X) / (P1.X – P0.X);
                        KÜLÖNBEN
                            HA ((KOD_KINN ÉS 4) = IGAZ) AKKOR
                                X <- P0.X + (P1.X – P0.X) * (ABLAK.JOBB – P0.Y) / (P1.Y – P0.Y);
                                Y <- ABLAK.FONT;
                            KÜLÖNBEN
                                HA ((KOD_KINN ÉS 8) = IGAZ) AKKOR
                                    X <- P0.X + (P1.X – P0.X) * (ABLAK.JOBB – P0.Y) / (P1.Y – P0.Y);
                                    Y <- ABLAK.LENT;
                                HA_VÉGE;
                            HA_VÉGE;
                        HA_VÉGE;
                    HA_VÉGE;
                
                    HA (KOD0 = IGAZ) AKKOR
                        P0.X <- X;
                        P0.Y <- Y;
                        KOD0 <- VEGPONT_KOD(P0);
                    KÜLÖNBEN
                        P1.X <- X;
                        P1.Y <- Y;
                        KOD1 <- VEGPONT_KOD(P1);
                    HA_VÉGE;
                HA_VÉGE;
            HA_VÉGE;
        CIKLUS_VÉGE;

        HA (ELFOGAD = IGAZ) AKKOR
            SZAKASZ(P0, P1);
        HA_VÉGE;

ELJÁRÁS_VÉGE;
```

Bezier alapjai
- Ismerni kell a kezdő- és a végpontot, ill. egy ún. vezérlőpontot, amitől a görbe tulajdonképpeni alakja függeni fog. A jobboldali ábrán a kezdőpont A, a végpont B, a vezérlőpont pedig V betűvel van jelölve.

- A görbe kirajzolása a következőképpen zajlik:

  - összekötjük a végpontokat a vezérlőponttal (AV és BV szakaszok)
  - az így kapott szakaszok felezőpontját (P és Q) is összekötjük
  - a PQ szakasz felezőpontja (X) a görbe egy pontját adja
  - az eljárást újrakezdjük az A és X pontokra P vezérlőponttal ill. a B és X pontokra Q vezérlőponttal

![Bezier](./bezier.png)