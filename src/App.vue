<script setup>
import Airtable from 'airtable'

const airtable = new Airtable({
  apiKey: 'patc2FdeoPLdCTR9m.44b20d3bae47e8fa2a2764be3dafa1e022e2dee036759b664dd9d4cd4ce3f19f'
})
const base = airtable.base('app74FKaaw2gyqCs9')
const table = base('tbllF8DuqHNat7UCK')

const analysis = async () => {
  const text = document.querySelector('.form-control').value.trim()
  const items = document.querySelectorAll('.list-group-item')
  let delay = 1000

  if (text !== '') {
    document.querySelector('.list-group').style.display = 'block'

    setTimeout(() => {
      for (let i = 0; i < items.length; i++) {
        delay += 1000

        setTimeout(() => {
          items[i].classList.remove('placeholder')
        }, delay)
      }
    }, 2000)

    await table.create({
      Text: text
    })
  }
}
</script>

<template>
  <div class="container">
    <img src="./assets/logo.png" alt="logo" />
    <h3>
      개발 요구사항을 입력하시면<br />
      AI가 분석해서 수정된 요구사항을<br />
      추천해드립니다.
    </h3>
    <form onsubmit="return false;">
      <input
        type="text"
        class="form-control margin-top-20"
        placeholder="버튼을 만들어주세요."
        required
      />
      <button type="submit" class="btn btn-primary margin-top-20" @click="analysis">
        분석하기
      </button>
    </form>
    <section>
      <ol class="list-group list-group-numbered placeholder-glow margin-top-20">
        <li class="list-group-item placeholder w-100">submit 버튼을 만들어주세요.</li>
        <li class="list-group-item placeholder w-100">reset 버튼을 만들어주세요.</li>
        <li class="list-group-item placeholder w-100">button 버튼을 만들어주세요.</li>
      </ol>
    </section>
  </div>
</template>

<style scoped>
.margin-top-20 {
  margin-top: 20px;
}
.container {
  text-align: center;
}
.list-group {
  display: none;
}
</style>
