#  Documentation of my best project


## Generator Maintainer - INTERNAL PROJECT THAT LED TO MY PROMOTION (2025)

![Generator Maintainer Screenshot](image.png)

A tool for managing generator systems. I mainly worked on the backend but sometimes contributed to frontend features.  

**Favorite Piece of Code (Frontend):** Cursor-based pagination for navigating generator readings smoothly.

```typescript
const [params, setParams] = useState<ReadingsParams>({
  startDate: new Date(),
  endDate: new Date(),
  limit: PAGE_LIMIT,
  gen: DEFAULT_GENS
});

const [cursorStack, setCursorStack] = useState<string[]>([]);

const handleNext = () => {
  if (data?.nextCursor) {
    setCursorStack([...cursorStack, params.cursor || ""]);
    setParams({ ...params, cursor: data.nextCursor });
  }
};

const handlePrevious = () => {
  const prevStack = [...cursorStack];
  const prevCursor = prevStack.pop();
  if (prevCursor !== undefined) {
    setCursorStack(prevStack);
    setParams({ ...params, cursor: prevCursor || undefined });
  }
};
```


## LITRAINER (2024) - OPEN SOURCE PASSION PROJECT THAT GAVE ME MY MOST LOVED AND IMPACTFUL PROJECT

<img width="1910" height="913" alt="image" src="https://github.com/user-attachments/assets/c4daaf8b-b126-48f3-86c1-ca3d329e5d73" />


A ReactJS app that uses Stockfish and the Lichess API to turn mistakes from online chess games into personalized learning puzzles.  

**Favorite Piece of Code (Experiment Start):** This snippet is where I realized I could leverage this data to create a chess site


```typescript
import { Chess } from "chess.js";
import openings from "./openings";
import { LichessEvaluation, LichessGameResponse, Puzzle, PositionOpening } from "@/typing/interfaces";
import { GamePhase } from "@/typing/enums";

export const parseGames = async (response: Response) => {
  if (!response.body) return;

  const reader = response.body.getReader();
  const decoder = new TextDecoder();
  let result = "";
  let chunk;

  while (!(chunk = await reader.read()).done) {
    result += decoder.decode(chunk.value, { stream: true });
  }

  const games = result.split("\n").filter((g) => g.trim() !== "");
  const evaluations: string[] = games.map((g) => JSON.parse(g).analysis);

  const parsedGames: LichessGameResponse[] = games.map((line) => {
    const game = JSON.parse(line);
    return {
      players: game.players,
      moves: game.moves,
      game_id: game.id,
      fen: game.fen,
      perf: game.perf,
      rated: game.rated,
      status: game.status,
      variant: game.variant,
      clock: game.clock,
      winner: game.winner,
      opening: game.opening,
      division: game.division
    };
  });

  return { evaluations, games: parsedGames };
};
```



