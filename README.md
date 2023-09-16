```
interface User {
  id: string
  username: string
  active: boolean
}

type State = {
  users: Record<string, User>
}

type Actions = {
  toggleActive: (userId: string) => void
}

export type UserState = State & Actions;

const UserState = immer<UserState>((set, get, api) => ({
  users: {
    '82471c5f-4207-4b1d-abcb-b98547e01a3e': {
      id: '82471c5f-4207-4b1d-abcb-b98547e01a3e',
      username: 'Learn Zustand',
      active: false,
    },
    '354ee16c-bfdd-44d3-afa9-e93679bda367': {
      id: '354ee16c-bfdd-44d3-afa9-e93679bda367',
      username: 'Learn Jotai',
      active: false,
    },
  },
  toggleActive: (userId: string) =>
    set((state) => {
      state.users[userId].active = !state.users[userId].active
    }),
}));

const UNIQUE_USERS_KEY = 'user-storage'


export const persistUsersState = persist(UserState, {
  name: UNIQUE_USERS_KEY,
  storage: createJSONStorage(() => AsyncStorage),
  onRehydrateStorage: () => (state) => {
  }
})

export const useUsersStore = create<State & Actions>()(persistUsersState)
```
