<script setup lang="ts">
import { computed, ref } from 'vue'

const customer = ref({
  name: '',
  cpf: '',
  email: '',
  password: ''
})

const active = computed(() => {
  /* EXERCÍCIO 1 (0.5 pontos a serem adicionados na avaliação 1)

     - Faça um formulário com 4 campos: nome, cpf, email e senha e um botão de salvar
     - O botão de salvar só pode ser habilitado com as seguintes condições:
     -  1. todos os campos preenchidos
     -  2. o campo senha deve ter no mínimo 8 caracteres contendo:
     -  2.1 no mínimo 1 maiúscula, 1 minúscula, 1 número e 1 caracter especial.
     -  2.2 deve haver uma lista indicando que cada regra da senha foi cumprido ou não.

    dica: utilize regex ou não.
*/
  const validPassword =
    customer.value.password.length > 8 &&
    customer.value.password.match(/[A-Z]/g) &&
    customer.value.password.match(/[a-z]/g) &&
    customer.value.password.match(/[^A-z 0-9]/g) &&
    customer.value.password.match(/[0-9]/g)

  return customer.value.name && customer.value.cpf && customer.value.email && validPassword
})

const submit = ref(() => {
  console.log('salvando...')
})


</script>

<template>
  <main class="min-h-screen flex flex-col items-center justify-center">
    <h1 class="text-2xl font-bold mb-4">Cadastro</h1>
    <div class="flex flex-col w-64 gap-2">
      <input
        type="text"
        v-model="customer.name"
        placeholder="Nome Completo"
        class="text-neutral-900 placeholder:text-neutral-500 bg-neutral-100 rounded px-2 py-1"
      />
      <input
        type="text"
        v-model="customer.cpf"
        placeholder="CPF"
        class="text-neutral-900 placeholder:text-neutral-500 bg-neutral-100 rounded px-2 py-1"
      />
      <input
        type="email"
        v-model="customer.email"
        placeholder="E-mail"
        class="text-neutral-900 placeholder:text-neutral-500 bg-neutral-100 rounded px-2 py-1"
      />
      <input
        type="password"
        v-model="customer.password"
        placeholder="Senha"
        class="text-neutral-900 placeholder:text-neutral-500 bg-neutral-100 rounded px-2 py-1"
      />
      <ul :class="customer.password ? 'block' : 'hidden'">
        <li
          :class="customer.password.length > 8 ? 'text-green-400' : 'line-through text-neutral-400'"
        >
          8 ou mais caracteres
        </li>
        <li
          :class="
            customer.password.match(/[A-Z]/g) ? 'text-green-400' : 'line-through text-neutral-400'
          "
        >
          1+ letra maiúscula
        </li>
        <li
          :class="
            customer.password.match(/[a-z]/g) ? 'text-green-400' : 'line-through text-neutral-400'
          "
        >
          1+ letra minúscula
        </li>
        <li
          :class="
            customer.password.match(/[^A-z 0-9]/g)
              ? 'text-green-400'
              : 'line-through text-neutral-400'
          "
        >
          1+ caracter especial
        </li>
        <li
          :class="
            customer.password.match(/[0-9]/g) ? 'text-green-400' : 'line-through text-neutral-400'
          "
        >
          1+ número
        </li>
      </ul>
      <button
        :class="
          active
            ? 'bg-green-600 font-bold rounded cursor-pointer py-1'
            : 'bg-red-600 font-bold rounded cursor-not-allowed py-1'
        "
        :disabled="!active"
        @click="submit"
      >
        Salvar
      </button>
    </div>
  </main>
</template>
