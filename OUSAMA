# il faut utiliser la fonction reason de chatgpt avec la prompt suivante :On a une figure géométrique en ASCII. La figure doit être entouré de "x" c'est a dire les chaines de caractère à une et deux unités de distances de l'extérieur de la figure sont des "x". Tu dois également supprimer les caractères formant la figure de bases. Ne met pas de "x" à l'intérieur de la figure. Ecrit ce programme en python

def surround_figure_with_x(figure_lines):
    """
    Prend en entrée la figure ASCII sous forme de liste de chaînes.
    Retourne la figure avec la bordure de x (2 couches)
    en supprimant les caractères d'origine.
    """
    # Dimensions de la figure d'origine
    original_height = len(figure_lines)
    original_width = max(len(line) for line in figure_lines)
    
    # On ajoute un padding de 2 lignes/colonnes de chaque côté pour être sûr de pouvoir dessiner la bordure.
    padded_height = original_height + 4
    padded_width = original_width + 4
    
    # Créer une grille (tableau 2D) initialement remplie d'espaces
    grid = [[' ' for _ in range(padded_width)] for _ in range(padded_height)]
    
    # On place la figure dans la grille en décalant de 2 (padding)
    # On considère qu'une case fait partie de la figure si le caractère n'est pas un espace.
    figure_set = set()
    for i, line in enumerate(figure_lines):
        for j, ch in enumerate(line):
            if ch != ' ':
                grid[i + 2][j + 2] = ch
                figure_set.add((i + 2, j + 2))
    
    # Déterminer le contour de la figure.
    # Une case (i, j) de la figure est sur le contour si l'un de ses voisins (8 directions)
    # n'appartient pas à la figure (ou est hors limites).
    boundary_set = set()
    for (i, j) in figure_set:
        for di in [-1, 0, 1]:
            for dj in [-1, 0, 1]:
                if di == 0 and dj == 0:
                    continue
                ni, nj = i + di, j + dj
                # Si le voisin est hors limites ou n'est pas dans la figure, alors (i,j) est sur le contour.
                if not (0 <= ni < padded_height and 0 <= nj < padded_width) or ((ni, nj) not in figure_set):
                    boundary_set.add((i, j))
                    # On peut arrêter les vérifications pour cette case
                    break
            else:
                continue
            break

    # On va maintenant déterminer la "bordure" :
    # Ce sont toutes les cases qui ne font pas partie de la figure et qui se trouvent
    # à exactement 1 ou 2 cases (distance Chebyshev) d'au moins une case du contour.
    border_set = set()
    for (i, j) in boundary_set:
        for di in range(-2, 3):
            for dj in range(-2, 3):
                # On veut une distance exactement 1 ou 2 (c'est-à-dire max(|di|,|dj|) vaut 1 ou 2)
                if max(abs(di), abs(dj)) in (1, 2):
                    ni, nj = i + di, j + dj
                    if 0 <= ni < padded_height and 0 <= nj < padded_width:
                        if (ni, nj) not in figure_set:
                            border_set.add((ni, nj))
                            
    # Construire le résultat : dans la grille de sortie, on place un "x" sur chaque case de la bordure
    # et on laisse un espace ailleurs.
    output_grid = [[' ' for _ in range(padded_width)] for _ in range(padded_height)]
    for (i, j) in border_set:
        output_grid[i][j] = 'x'
        
    # On retourne le résultat sous forme de liste de chaînes
    output_lines = [''.join(row) for row in output_grid]
    return output_lines


if __name__ == '__main__':
    # Exemple de figure ASCII (vous pouvez remplacer cette figure par celle de votre choix)
    figure = [
        "   *****   ",
        "   *   *   ",
        "   *   *   ",
        "   *****   "
    ]
    
    result = surround_figure_with_x(figure)
    for line in result:
        print(line)
